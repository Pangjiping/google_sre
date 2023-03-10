## **Indicators in Practice**

## **实践中的SLI**

Given that we’ve made the case for why choosing appropriate metrics to measure your service is important, how do you go about identifying what metrics are meaningful to your service or system?

鉴于我们已经说明了为什么选择适当的指标来衡量你的服务是重要的，你如何去确定哪些指标对你的服务或系统是有意义的？

<br>

### **What Do You and Your Users Care About?**

### **你和你的用户关心的是什么？**

You shouldn’t use every metric you can track in your monitoring system as an SLI; an understanding of what your users want from the system will inform the judicious selection of a few indicators. Choosing too many indicators makes it hard to pay the right level of attention to the indicators that matter, while choosing too few may leave significant behaviors of your system unexamined. We typically find that a handful of representative indicators are enough to evaluate and reason about a system’s health.

你不应该把监控系统中可以追踪的每一个指标都作为SLI；对用户希望从系统中得到什么的理解将为明智地选择一些指标提供依据。选择太多的指标会使你很难对重要的指标给予正确的关注，而选择太少的指标可能会使你的系统的重要行为没有得到审查。我们通常发现，少数几个有代表性的指标就足以评估和推理一个系统的健康状况。

Services tend to fall into a few broad categories in terms of the SLIs they find relevant:

* User-facing serving systems, such as the Shakespeare search frontends, generally care about availability, latency, and throughput. In other words: Could we respond to the request? How long did it take to respond? How many requests could be handled?
* Storage systems often emphasize latency, availability, and durability. In other words: How long does it take to read or write data? Can we access the data on demand? Is the data still there when we need it? See Chapter 26 for an extended discussion of these issues.
* Big data systems, such as data processing pipelines, tend to care about throughput and end-to-end latency. In other words: How much data is being processed? How long does it take the data to progress from ingestion to completion? (Some pipelines may also have targets for latency on individual processing stages.)
* All systems should care about correctness: was the right answer returned, the right data retrieved, the right analysis done? Correctness is important to track as an indicator of system health, even though it’s often a property of the data in the system rather than the infrastructure per se, and so usually not an SRE responsibility to meet.

在他们认为相关的SLI方面，服务往往分为几大类：

* 面向用户的服务系统，如Shakespeare的搜索前端，通常关心可用性、延迟和吞吐量。换句话说。我们能否对请求作出回应？响应需要多长时间？可以处理多少个请求？
* 存储系统通常强调延迟、可用性和持久性。换句话说。读取或写入数据需要多长时间？我们能否按需访问数据？当我们需要它时，数据是否还在那里？关于这些问题的详细讨论，见第26章。
* 大数据系统，如数据处理流水线，往往关心吞吐量和端到端的延迟。换句话说。有多少数据正在被处理？数据从摄入到完成需要多长时间？（一些流水线可能也有个别处理阶段的延迟目标）。
* 所有的系统都应该关心正确性：是否返回了正确的答案，检索了正确的数据，做了正确的分析？正确性作为系统健康的一个指标是很重要的，尽管它通常是系统中数据的一个属性，而不是基础设施本身，所以通常不是SRE的责任。

<br>

### **Collecting Indicators**

### **采集指标**

Many indicator metrics are most naturally gathered on the server side, using a monitoring system such as Borgmon (see Chapter 10) or Prometheus, or with periodic log analysis—for instance, HTTP 500 responses as a fraction of all requests. However, some systems should be instrumented with client-side collection, because not measuring behavior at the client can miss a range of problems that affect users but don’t affect server-side metrics. For example, concentrating on the response latency of the Shakespeare search backend might miss poor user latency due to problems with the page’s JavaScript: in this case, measuring how long it takes for a page to become usable in the browser is a better proxy for what the user actually experiences.

许多指标是在服务器端收集的，使用Borgmon（见第10章）或Prometheus等监控系统，或通过定期的日志分析--例如，HTTP 500响应作为所有请求的一部分。然而，有些系统应该用客户端采集的工具，因为不测量客户端的行为会错过一系列影响用户但不影响服务器端指标的问题。例如，专注于Shakespeare搜索后台的响应延迟可能会错过由于页面的JavaScript问题而导致的糟糕的用户延迟：在这种情况下，测量页面在浏览器中成为可用的时间是用户实际体验的更好的代理。

<br>

### **Aggregation**

### **汇总**

For simplicity and usability, we often aggregate raw measurements. This needs to be done carefully.

为了简单和方便使用，我们经常将原始的测量结果汇总。这需要谨慎行事。

Some metrics are seemingly straightforward, like the number of requests per second served, but even this apparently straightforward measurement implicitly aggregates data over the measurement window. Is the measurement obtained once a second, or by averaging requests over a minute? The latter may hide much higher instantaneous request rates in bursts that last for only a few seconds. Consider a system that serves 200 requests/s in even-numbered seconds, and 0 in the others. It has the same average load as one that serves a constant 100 requests/s, but has an instantaneous load that is twice as large as the average one. Similarly, averaging request latencies may seem attractive, but obscures an important detail: it’s entirely possible for most of the requests to be fast, but for a long tail of requests to be much, much slower.

有些指标看起来很直接，比如每秒服务的请求数，但即使是这种明显直接的测量也隐含着对测量窗口的数据汇总。是一秒钟一次的测量，还是通过对一分钟内的请求进行平均来获得？后者可能隐藏了更高的瞬时请求率，只持续了几秒钟。考虑一个在偶数秒内提供200个请求/秒的系统，而在其他秒内提供0个请求/秒。它的平均负载与提供恒定的100个请求/s的系统相同，但其瞬时负载是平均负载的两倍。同样，平均请求延迟看起来很有吸引力，但却掩盖了一个重要的细节：大多数请求是快速的，但长请求却慢得多，这是完全可能的。

Most metrics are better thought of as distributions rather than averages. For example, for a latency SLI, some requests will be serviced quickly, while others will invariably take longer—sometimes much longer. A simple average can obscure these tail latencies, as well as changes in them. Figure 4-1 provides an example: although a typical request is served in about 50 ms, 5% of requests are 20 times slower! Monitoring and alerting based only on the average latency would show no change in behavior over the course of the day, when there are in fact significant changes in the tail latency (the topmost line).

大多数指标最好被认为是分布，而不是平均数。例如，对于延迟SLI，一些请求会很快得到服务，而另一些请求总是需要更长的时间，有时甚至更长。一个简单的平均数可能会掩盖这些尾部延迟，以及它们的变化。Figure 4-1提供了一个例子：尽管一个典型的请求在50毫秒内得到服务，但有5%的请求却慢了20倍。仅仅基于平均延迟的监控和警报会显示一天中的行为没有变化，而事实上，尾部延迟（最上面的一行）有明显的变化。

![50th, 85th, 95th, and 99th percentile latencies for a system. Note that the Y- axis has a logarithmic scale.
](./figures/4-1.png)
> Figure 4-1. 50th, 85th, 95th, and 99th percentile latencies for a system. Note that the Y- axis has a logarithmic scale.

Using percentiles for indicators allows you to consider the shape of the distribution and its differing attributes: a high-order percentile, such as the 99th or 99.9th, shows you a plausible worst-case value, while using the 50th percentile (also known as the median) emphasizes the typical case. The higher the variance in response times, the more the typical user experience is affected by long-tail behavior, an effect exacerbated at high load by queuing effects. User studies have shown that people typically prefer a slightly slower system to one with high variance in response time, so some SRE teams focus only on high percentile values, on the grounds that if the 99.9th percentile behavior is good, then the typical experience is certainly going to be.

使用百分位数作为指标，可以考虑分布的形状及其不同的属性：高阶百分位数，如第99位或99.9位，向你展示一个可信的最坏情况下的数值，而使用第50位百分位数（也称为中位数）则强调典型情况。响应时间的差异越大，典型的用户体验受长尾行为的影响就越大，这种影响在高负载时因排队效应而加剧。用户研究表明，人们通常喜欢稍微慢一点的系统，而不是响应时间差异大的系统，所以一些SRE团队只关注高百分位数的数值，理由是如果99.9百分位数的行为是好的，那么典型的体验肯定也是好的。

<br>

### **Standardize Indicators**

### **标准化指标**

We recommend that you standardize on common definitions for SLIs so that you don’t have to reason about them from first principles each time. Any feature that conforms to the standard definition templates can be omitted from the specification of an individual SLI, e.g.:

* Aggregation intervals: "Averaged over 1 minute"
* Aggregation regions: "All the tasks in a cluster"
* How frequently measurements are made: "Every 10 seconds"
* Which requests are included: "HTTP GETs from black-box monitoring jobs"
* How the data is acquired: "Through our monitoring, measured at the server"
* Data-access latency: "Time to last byte"

我们建议你对SLI的通用定义进行标准化，这样你就不必每次都从第一原则出发进行推理。任何符合标准定义模板的功能都可以从单个SLI的规范中省略，例如：

* 汇总时间间隔。“1分钟的平均数”
* 汇总范围。“一个集群中的所有任务”
* 测量的频率如何。“每10秒”
* 哪些请求被包括在内。“来自黑盒监测工作的HTTP GETs”
* 数据是如何获得的。“通过我们的监测，在服务器上测量”
* 数据访问延迟。“到最后一个字节的时间”

To save effort, build a set of reusable SLI templates for each common metric; these also make it simpler for everyone to understand what a specific SLI means.

为了节省精力，为每个通用指标建立一套可重复使用的SLI模板；这些模板也使每个人更容易理解特定SLI的含义。

<br>

---

**[Back to contents of the chapter（返回章节目录）](service_level_objectives.md)**

* **Previous Section（上一节）：[Service Level Terminology（服务水平术语）](service_level_terminology.md)**
* **Next Section（下一节）：[Objectives in Practice（实践中的SLO）](objectives_in_practice.md)**
