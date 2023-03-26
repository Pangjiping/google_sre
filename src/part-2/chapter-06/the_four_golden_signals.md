## **The Four Golden Signals**

## **四种黄金信号**

The four golden signals of monitoring are latency, traffic, errors, and saturation. If you can only measure four metrics of your user-facing system, focus on these four.

监测的四个黄金信号是延迟、流量、错误和饱和度。如果你只能测量面向用户的系统的四个指标，那么请关注这四个指标。

**Latency**

The time it takes to service a request. It’s important to distinguish between the latency of successful requests and the latency of failed requests. For example, an HTTP 500 error triggered due to loss of connection to a database or other critical backend might be served very quickly; however, as an HTTP 500 error indicates a failed request, factoring 500s into your overall latency might result in misleading calculations. On the other hand, a slow error is even worse than a fast error! Therefore, it’s important to track error latency, as opposed to just filtering out errors.

**延迟**

为一个请求提供服务所需的时间。区分成功请求的延时和失败请求的延时是很重要的。例如，由于与数据库或其他关键后端失去连接而触发的HTTP 500错误可能会很快得到服务；然而，由于HTTP 500错误表示一个失败的请求，将500的因素计入你的整体延迟可能会导致误导的计算。另一方面，一个慢的错误甚至比一个快的错误更糟糕！因此，跟踪一个慢的错误很重要。因此，跟踪错误延迟是很重要的，而不是仅仅过滤掉错误。

**Traffic**

A measure of how much demand is being placed on your system, measured in a high-level system-specific metric. For a web service, this measurement is usually HTTP requests per second, perhaps broken out by the nature of the requests (e.g., static versus dynamic content). For an audio streaming system, this measurement might focus on network I/O rate or concurrent sessions. For a key-value storage system, this measurement might be transactions and retrievals per second.

**流量**

衡量对你的系统的需求有多大，以高层次的系统特定指标来衡量。对于网络服务来说，这种测量通常是每秒的HTTP请求，也许可以根据请求的性质来细分（例如，静态与动态内容）。对于一个音频流系统，这种测量可能集中在网络I/O率或并发会话上。对于一个键值存储系统，这种测量可能是每秒的交易和检索。

**Errors**

The rate of requests that fail, either explicitly (e.g., HTTP 500s), implicitly (for example, an HTTP 200 success response, but coupled with the wrong content), or by policy (for example, "If you committed to one-second response times, any request over one second is an error"). Where protocol response codes are insufficient to express all failure conditions, secondary (internal) protocols may be necessary to track partial failure modes. Monitoring these cases can be drastically different: catching HTTP 500s at your load balancer can do a decent job of catching all completely failed requests, while only end-to-end system tests can detect that you’re serving the wrong content.

**错误**

失败的请求率，可以是显性的（例如HTTP 500），隐性的（例如HTTP 200成功响应，但加上错误的内容），或通过协议（例如，“如果你承诺一秒钟的响应时间，任何超过一秒钟的请求都是错误”）。当协议响应代码不足以表达所有的故障情况时，可能需要二级（内部）协议来跟踪部分故障模式。监控这些情况可能会有很大的不同：在你的负载均衡器上捕捉HTTP 500可以很好地捕捉所有完全失败的请求，而只有端到端的系统测试可以检测到你正在提供错误的内容。

**Saturation**

How "full" your service is. A measure of your system fraction, emphasizing the resources that are most constrained (e.g., in a memory-constrained system, show memory; in an I/O-constrained system, show I/O). Note that many systems degrade in performance before they achieve 100% utilization, so having a utilization target is essential.

In complex systems, saturation can be supplemented with higher-level load measurement: can your service properly handle double the traffic, handle only 10% more traffic, or handle even less traffic than it currently receives? For very simple services that have no parameters that alter the complexity of the request (e.g., "Give me a nonce" or "I need a globally unique monotonic integer") that rarely change configuration, a static value from a load test might be adequate. As discussed in the previous paragraph, however, most services need to use indirect signals like CPU utilization or network bandwidth that have a known upper bound. Latency increases are often a leading indicator of saturation. Measuring your 99th percentile response time over some small window (e.g., one minute) can give a very early signal of saturation.

Finally, saturation is also concerned with predictions of impending saturation, such as "It looks like your database will fill its hard drive in 4 hours."

**饱和状态**

你的服务有多“满”。对你的系统部分的衡量，强调最受限制的资源（例如，在一个内存受限的系统中，显示内存；在一个I/O受限的系统中，显示I/O）。请注意，许多系统在达到100%的利用率之前就会出现性能下降，所以有一个利用率目标是非常重要的。

在复杂的系统中，饱和度可以用更高层次的负载测量来补充：你的服务可以适当地处理双倍的流量，只处理10%的流量，或者处理比它目前收到的更少的流量？对于非常简单的服务，没有改变请求复杂性的参数（例如，“给我一个nonce”或“我需要一个全局唯一的单调整数”），很少改变配置，来自负载测试的静态值可能已经足够。然而，正如上一段所讨论的，大多数服务需要使用间接信号，如CPU利用率或网络带宽，它们有一个已知的上限。延迟的增加往往是饱和的一个领先指标。测量你在某个小窗口（例如一分钟）的第99百分位响应时间，可以提供一个非常早期的饱和信号。

最后，饱和度还涉及到对即将到来的饱和度的预测，例如“看起来你的数据库将在4小时内填满它的硬盘”。

If you measure all four golden signals and page a human when one signal is problematic (or, in the case of saturation, nearly problematic), your service will be at least decently covered by monitoring.

如果你测量所有四个黄金信号，并在一个信号出现问题（或者在饱和的情况下，几乎出现问题）时呼叫人，那么你的服务至少会被监控覆盖得很好。

<br>

---

**[Back to contents of the chapter（返回章节目录）](monitoring_distributed_systems.md)**

* **Previous Section（上一节）：[Black-Box Versus White-Box（黑盒与白盒）](black-box_versus_white-box.md)**
* **Next Section（下一节）：[Worrying About Your Tail (or, Instrumentation and Performance)（小心拖尾数据（或者，仪表和性能））](worrying_about_your_tail.md)**
