## **Service Level Terminology**

## **服务水平术语**

Many readers are likely familiar with the concept of an SLA, but the terms SLI and SLO are also worth careful definition, because in common use, the term SLA is overloaded and has taken on a number of meanings depending on context. We prefer to separate those meanings for clarity.

许多读者可能对SLA的概念很熟悉，但SLI和SLO这两个术语也值得仔细定义，因为在通常的使用中，SLA这个词的含义过多，而且根据上下文的不同，有很多的含义。为了清楚起见，我们倾向于将这些含义分开。

<br>

### **Indicators**

### **服务水平指标**

An SLI is a service level indicator—a carefully defined quantitative measure of some aspect of the level of service that is provided.

SLI是一个服务水平指标--对所提供的服务水平的某些方面进行仔细定义的定量衡量。

Most services consider request latency—how long it takes to return a response to a request—as a key SLI. Other common SLIs include the error rate, often expressed as a fraction of all requests received, and system throughput, typically measured in requests per second. The measurements are often aggregated: i.e., raw data is collected over a measurement window and then turned into a rate, average, or percentile.

大多数服务将请求延迟--返回一个请求的响应所需的时间--视为一个关键的SLI。其他常见的SLI包括错误率，通常表示为收到的所有请求的一部分，以及系统吞吐量，通常以每秒请求数来衡量。测量通常是汇总的：即在一个测量窗口中收集原始数据，然后将其转化为比率、平均数或百分数。

Ideally, the SLI directly measures a service level of interest, but sometimes only a proxy is available because the desired measure may be hard to obtain or interpret. For example, client-side latency is often the more user-relevant metric, but it might only be possible to measure latency at the server.

理想情况下，SLI直接测量感兴趣的服务水平，但有时只能使用代理，因为所需的测量可能很难获得或解释。例如，客户端的延迟通常是与用户更相关的指标，但可能只有在服务器上才能测量延迟。

Another kind of SLI important to SREs is availability, or the fraction of the time that a service is usable. It is often defined in terms of the fraction of well-formed requests that succeed, sometimes called yield. (Durability—the likelihood that data will be retained over a long period of time—is equally important for data storage systems.) Although 100% availability is impossible, near-100% availability is often readily achievable, and the industry commonly expresses high-availability values in terms of the number of "nines" in the availability percentage. For example, availabilities of 99% and 99.999% can be referred to as "2 nines" and "5 nines" availability, respectively, and the current published target for Google Compute Engine availability is "three and a half nines"—99.95% availability.

另一种对SRE很重要的SLI是可用性，即服务可用的时间比例。它通常被定义为成功的格式良好的请求的百分比，有时称为产量。（持久性--数据被长期保留的可能性，对数据存储系统同样重要）。尽管100%的可用性是不可能的，但接近100%的可用性通常是可以实现的，业界通常用可用性百分比中的“9”的数量来表示高可用性的值。例如，99%和99.999%的可用性可以分别称为“2个9”和“5个9”，而目前公布的谷歌计算引擎可用性目标是“3个半9”--99.95%的可用性。

<br>

### **Objectives**

### **服务水平目标**

An SLO is a service level objective: a target value or range of values for a service level that is measured by an SLI. A natural structure for SLOs is thus SLI ≤ target or lower bound ≤ SLI ≤ upper bound. For example, we might decide that we will return Shakespeare search results "quickly," adopting an SLO that our average search request latency should be less than 100 milliseconds.

SLO是一个服务水平目标：一个由SLI衡量的服务水平的目标值或值范围。因此，SLO的一个自然结构是SLI≤目标或下限≤SLI≤上限。例如，我们可能决定要“快速”返回Shakespeare的搜索结果，采用一个SLO，即我们的平均搜索请求延迟应小于100毫秒。

Choosing an appropriate SLO is complex. To begin with, you don’t always get to choose its value! For incoming HTTP requests from the outside world to your service, the queries per second (QPS) metric is essentially determined by the desires of your users, and you can’t really set an SLO for that.

选择一个适当的SLO是复杂的。首先，你并不总是能够选择它的值 对于从外界传入你的服务的HTTP请求，每秒查询次数（QPS）指标基本上是由你的用户的愿望决定的，你不能真的为它设置一个SLO。

On the other hand, you can say that you want the average latency per request to be under 100 milliseconds, and setting such a goal could in turn motivate you to write your frontend with low-latency behaviors of various kinds or to buy certain kinds of low-latency equipment. (100 milliseconds is obviously an arbitrary value, but in general lower latency numbers are good. There are excellent reasons to believe that fast is better than slow, and that user-experienced latency above certain values actually drives people away— see "Speed Matters" [Bru09] for more details.)

另一方面，你可以说你希望每个请求的平均延迟在100毫秒以下，设定这样一个目标可以反过来激励你用各种低延迟的行为来编写你的前端，或者购买某些类型的低延迟设备。（100毫秒显然是一个任意的值，但一般来说，较低的延迟数字是好的。有很好的理由相信，快比慢好，而且用户体验到的超过一定值的延迟实际上会驱使人们离开--更多的细节见“速度问题”[Bru09]）。

Again, this is more subtle than it might at first appear, in that those two SLIs—QPS and latency—might be connected behind the scenes: higher QPS often leads to larger latencies, and it’s common for services to have a performance cliff beyond some load threshold.

同样，这比最初看起来更微妙，因为SLI-QPS和延迟可能在幕后有联系：更高的QPS往往导致更大的延迟，而且服务在超过某些负载阈值时，通常会出现性能悬崖。

Choosing and publishing SLOs to users sets expectations about how a service will perform. This strategy can reduce unfounded complaints to service owners about, for example, the service being slow. Without an explicit SLO, users often develop their own beliefs about desired performance, which may be unrelated to the beliefs held by the people designing and operating the service. This dynamic can lead to both over- reliance on the service, when users incorrectly believe that a service will be more available than it actually is (as happened with Chubby: see "The Global Chubby Planned Outage"), and under-reliance, when prospective users believe a system is flakier and less reliable than it actually is.

选择并向用户发布SLO设定了对服务性能的期望。这种策略可以减少对服务所有者的毫无根据的抱怨，比如说，服务很慢。如果没有明确的SLO，用户往往会发展他们自己对期望性能的信念，而这些信念可能与设计和运营服务的人所持有的信念无关。这种动态可能会导致对服务的过度依赖，当用户错误地认为一个服务会比实际情况更可用（就像Chubby发生的那样：见“全球Chubby计划性中断”），而当潜在的用户认为一个系统比实际情况更脆弱、更不可靠时，则会导致对服务的不足。

> **The Global Chubby Planned Outage**
>
> **全球Chubby计划性中断**
>
> Written by Marc Alvidrez
>
> Chubby [Bur06] is Google’s lock service for loosely coupled distributed systems. In the global case, we distribute Chubby instances such that each replica is in a different geographical region. Over time, we found that the failures of the global instance of Chubby consistently generated service outages, many of which were visible to end users. As it turns out, true global Chubby outages are so infrequent that service owners began to add dependencies to Chubby assuming that it would never go down. Its high reliability provided a false sense of security because the services could not function appropriately when Chubby was unavailable, however rarely that occurred.
>
> Chubby[Bur06]是谷歌为松耦合的分布式系统提供的锁服务。在全球范围内，我们分布Chubby实例，使每个副本都在不同的地理区域。随着时间的推移，我们发现Chubby的全球实例的故障持续产生了服务中断，其中许多对终端用户来说是可见的。事实证明，真正的全球Chubby中断是如此的不频繁，以至于服务所有者开始向Chubby添加依赖，认为它永远不会中断。它的高可靠性提供了一种虚假的安全感，因为当Chubby不可用时，服务就无法正常运行，无论这种情况发生得多么少。
>
> The solution to this Chubby scenario is interesting: SRE makes sure that global Chubby meets, but does not significantly exceed, its service level objective. In any given quarter, if a true failure has not dropped availability below the target, a controlled outage will be synthesized by intentionally taking down the system. In this way, we are able to flush out unreasonable dependencies on Chubby shortly after they are added. Doing so forces service owners to reckon with the reality of distributed systems sooner rather than later.
>
> Chubby的解决方案很有意思。SRE确保全球Chubby满足，但不明显超过其服务水平目标。在任何一个季度，如果一个真正的故障没有使可用性下降到目标以下，将通过故意关闭系统来合成一个受控的停工。通过这种方式，我们能够在Chubby上添加不合理的依赖关系后不久就将其排除在外。这样做迫使服务所有者尽早地考虑到分布式系统的现实。

<br>

### **Agreements**

### **服务水平协议**

Finally, SLAs are service level agreements: an explicit or implicit contract with your users that includes consequences of meeting (or missing) the SLOs they contain. The consequences are most easily recognized when they are financial—a rebate or a penalty—but they can take other forms. An easy way to tell the difference between an SLO and an SLA is to ask "what happens if the SLOs aren’t met?": if there is no explicit consequence, then you are almost certainly looking at an SLO.

最后，SLA是服务水平协议：与你的用户签订的明确或隐含的合同，包括达到（或错过）他们所包含的SLO的后果。这些后果在财务上最容易被识别--回扣或罚款，但它们也可以采取其他形式。区分SLO和SLA的一个简单方法是问“如果没有达到SLO会怎样？”：如果没有明确的后果，那么你几乎肯定是在看SLO。

SRE doesn’t typically get involved in constructing SLAs, because SLAs are closely tied to business and product decisions. SRE does, however, get involved in helping to avoid triggering the consequences of missed SLOs. They can also help to define the SLIs: there obviously needs to be an objective way to measure the SLOs in the agreement, or disagreements will arise.

SRE通常不参与构建SLA，因为SLA与业务和产品决策紧密相连。然而，SRE确实参与帮助避免触发SLO的后果。他们也可以帮助定义SLA：显然需要有一个客观的方法来衡量协议中的SLO，否则会产生分歧。

Google Search is an example of an important service that doesn’t have an SLA for the public: we want everyone to use Search as fluidly and efficiently as possible, but we haven’t signed a contract with the whole world. Even so, there are still consequences if Search isn’t available—unavailability results in a hit to our reputation, as well as a drop in advertising revenue. Many other Google services, such as Google for Work, do have explicit SLAs with their users. Whether or not a particular service has an SLA, it’s valuable to define SLIs and SLOs and use them to manage the service.

谷歌搜索是一个重要服务的例子，它对公众没有SLA：我们希望每个人都能尽可能流畅和有效地使用搜索，但我们没有与整个世界签署合同。即便如此，如果搜索不可用，仍然会有后果--不可用会导致我们的声誉受到打击，以及广告收入下降。许多其他的谷歌服务，如Google for Work，确实与他们的用户有明确的服务水平协议。无论一个特定的服务是否有SLA，定义SLA和SLO并使用它们来管理服务是很有价值的。

So much for the theory—now for the experience.

理论说了这么多，现在说说经验。

<br>

---

**[Back to contents of the chapter（返回章节目录）](service_level_objectives.md)**

* **Next Section（下一节）：[Indicators in Practice（实践中的SLI）](indicators_in_practice.md)**
