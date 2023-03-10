## **Risk Tolerance of Services**

## **服务的风险承受能力**

What does it mean to identify the risk tolerance of a service? In a formal environment or in the case of safety-critical systems, the risk tolerance of services is typically built directly into the basic product or service definition. At Google, services’ risk tolerance tends to be less clearly defined.

识别服务的风险风险承受能力是什么意思？在生产环境中或在安全关键系统的情况下，服务的风险承受能力通常直接建立在基本产品或服务定义中。在Google，服务的风险承受能力往往没有明确定义。

To identify the risk tolerance of a service, SREs must work with the product owners to turn a set of business goals into explicit objectives to which we can engineer. In this case, the business goals we’re concerned about have a direct impact on the performance and reliability of the service offered. In practice, this translation is easier said than done. While consumer services often have clear product owners, it is unusual for infrastructure services (e.g., storage systems or a general-purpose HTTP caching layer) to have a similar structure of product ownership. We’ll discuss the consumer and infrastructure cases in turn.

为了确定服务的风险承受能力，SRE必须与产品负责人合作，将一组业务目标转化为明确的目标，以便我们进行工程设计。在这种情况下，我们所关心的业务目标直接影响所提供的服务的性能和可靠性。实践中，这种转化说起来容易做起来难。虽然消费者服务通常有明确的产品负责人，但基础设施服务（例如，存储系统或通用HTTP缓存层）很少有类似的产品所有权结构。我们将依次讨论消费者和基础设施情况。

<br>

### **Identifying the Risk Tolerance of Consumer Services**

### **确定消费者服务的风险承受能力**

Our consumer services often have a product team that acts as the business owner for an application. For example, Search, Google Maps, and Google Docs each have their own product managers. These product managers are charged with understanding the users and the business, and for shaping the product for success in the marketplace. When a product team exists, that team is usually the best resource to discuss the reliability requirements for a service. In the absence of a dedicated product team, the engineers building the system often play this role either knowingly or unknowingly.

我们的消费者服务通常拥有一个产品团队，作为业务所有者。例如，搜索、Google地图和Google文档都有自己的产品经理。这些产品经理的职责是了解用户和业务，并塑造产品以在市场上取得成功。当存在产品团队时，该团队通常是讨论服务可靠性要求的最佳资源。在没有专门的产品团队的情况下，构建系统的工程师通常会有意或无意地担任此角色。

There are many factors to consider when assessing the risk tolerance of services, such as the following:

* What level of availability is required?
* Do different types of failures have different effects on the service?
* How can we use the service cost to help locate a service on the risk continuum?
* What other service metrics are important to take into account?

在评估服务的风险承受能力时，需要考虑许多因素，例如以下内容：

* 需要什么级别的可用性？
* 不同类型的故障对服务有不同的影响吗？
* 我们如何利用服务成本来帮助确定服务在风险连续体上的位置？
* 还有哪些服务指标需要考虑？

<br>

#### **Target level of availability**

#### **目标可用性水平**

The target level of availability for a given Google service usually depends on the function it provides and how the service is positioned in the marketplace. The following list includes issues to consider:

* What level of service will the users expect?
* Does this service tie directly to revenue (either our revenue, or our customers’ revenue)?
* Is this a paid service, or is it free?
* If there are competitors in the marketplace, what level of service do those competitors provide?
* Is this service targeted at consumers, or at enterprises?

给定Google服务的目标可用性水平通常取决于其提供的功能以及服务在市场中的定位。以下列表包括需要考虑的问题：

* 用户期望什么级别的服务？
* 该服务是否直接与收入挂钩（无论是我们的收入还是我们客户的收入）？
* 这是一个付费服务还是免费服务？
* 如果市场上有竞争对手，那些竞争对手提供什么水平的服务？
* 这项服务的目标是面向消费者还是企业？

Consider the requirements of Google Apps for Work. The majority of its users are enterprise users, some large and some small. These enterprises depend on Google Apps for Work services (e.g., Gmail, Calendar, Drive, Docs) to provide tools that enable their employees to perform their daily work. Stated another way, an outage for a Google Apps for Work service is an outage not only for Google, but also for all the enterprises that critically depend on us. For a typical Google Apps for Work service, we might set an external quarterly availability target of 99.9%, and back this target with a stronger internal availability target and a contract that stipulates penalties if we fail to deliver to the external target.

考虑Google Apps for Work的要求。其大多数用户是企业用户。这些企业依赖于Google Apps for Work服务（例如Gmail、日历、Drive、文档）提供工具，使其员工能够完成日常工作。换句话说，Google Apps for Work服务的故障不仅会影响Google自身，还会影响所有依赖我们的企业。对于典型的Google Apps for Work服务，我们可能会设置一个每季度99.9%的外部可用性目标，并以更强的内部可用性目标和一份规定了如果我们未能达到外部目标将会受到惩罚的合约来支持这一目标。

YouTube provides a contrasting set of considerations. When Google acquired YouTube, we had to decide on the appropriate availability target for the website. In 2006, YouTube was focused on consumers and was in a very different phase of its business lifecycle than Google was at the time. While YouTube already had a great product, it was still changing and growing rapidly. We set a lower availability target for YouTube than for our enterprise products because rapid feature development was correspondingly more important.

YouTube提供了一组对比的考虑因素。当Google收购YouTube时，我们必须决定该网站的适当可用性目标。2006年，YouTube专注于消费者，处于与当时的Google非常不同的业务生命周期阶段。虽然YouTube已经拥有了一个很棒的产品，但它仍在快速变化和成长。我们为YouTube设置了一个较低的可用性目标，因为快速的功能开发同样重要。

<br>

#### **Types of failures**

#### **故障类型**

The expected shape of failures for a given service is another important consideration. How resilient is our business to service downtime? Which is worse for the service: a constant low rate of failures, or an occasional full-site outage? Both types of failure may result in the same absolute number of errors, but may have vastly different impacts on the business.

给定服务的故障预期是另一个重要的考虑因素。我们的业务对服务停机有多弹性？对于服务来说，什么更糟糕：持续低故障率，还是偶发的全站点停机？两种类型的故障可能导致相同数量的错误，但对业务的影响可能大相径庭。

An illustrative example of the difference between full and partial outages naturally arises in systems that serve private information. Consider a contact management application, and the difference between intermittent failures that cause profile pictures to fail to render, versus a failure case that results in a user’s private contacts being shown to another user. The first case is clearly a poor user experience, and SREs would work to remediate the problem quickly. In the second case, however, the risk of exposing private data could easily undermine basic user trust in a significant way. As a result, taking down the service entirely would be appropriate during the debugging and potential clean-up phase for the second case.

在为私人信息提供服务的系统中，全站点停机和部分停机之间的区别可通过一个例子来说明。考虑一个联系人管理应用程序，以及导致个人资料图片无法渲染的间歇性故障与导致用户私人联系人被显示给另一个用户的故障之间的差异。第一种情况显然是糟糕的用户体验，SREs将会迅速解决问题。然而，在第二种情况下，暴露私人数据的风险很容易以重大的方式破坏用户的基本信任。因此，在第二种情况的调试和潜在清理阶段，完全关闭服务是适当的。

At the other end of services offered by Google, it is sometimes acceptable to have regular outages during maintenance windows. A number of years ago, the Ads Frontend used to be one such service. It is used by advertisers and website publishers to set up, configure, run, and monitor their advertising campaigns. Because most of this work takes place during normal business hours, we determined that occasional, regular, scheduled outages in the form of maintenance windows would be acceptable, and we counted these scheduled outages as planned downtime, not unplanned downtime.

在Google提供的服务中，有时在维护窗口期间定期停机是可以接受的。几年前，广告前端就是这样的一项服务。广告前端被广告主和网站发布者用于设置、配置、运行和监控他们的广告活动。由于大部分工作都在正常工作时间内进行，我们确定间歇性、定期、计划的停机在维护窗口的形式下是可以接受的，并且我们将这些计划的停机视为计划内的停机，而不是计划外的停机。

<br>

#### **Cost**

#### **成本**

Cost is often the key factor in determining the appropriate availability target for a service. Ads is in a particularly good position to make this trade-off because request successes and failures can be directly translated into revenue gained or lost. In determining the availability target for each service, we ask questions such as:

* If we were to build and operate these systems at one more nine of availability, what would our incremental increase in revenue be?
* Does this additional revenue offset the cost of reaching that level of reliability?

成本通常是确定服务适当可用性目标的关键因素。广告服务很好地进行这种权衡，因为请求成功和失败可以直接转化为获得或损失的收入。在确定每个服务的可用性目标时，我们会问一些问题，例如：

* 如果我们将这些系统的可用性提高一个数量级，我们的收入增量将是多少？
* 这种额外的收入是否抵消了达到这种可靠性水平的成本？

To make this trade-off equation more concrete, consider the following cost/benefit for an example service where each request has equal value:

* Proposed improvement in availability target: 99.9% → 99.99%
* Proposed increase in availability: 0.09%
* Service revenue: $1M
* Value of improved availability: $1M * 0.0009 = $900

为了使这种权衡方程更加具体化，考虑以下针对一个示例服务的成本/效益分析：

* 可用性目标的建议改进：从99.9%提高到99.99%
* 可用性的建议增加：0.09%
* 服务收入：1百万美元
* 提高可用性的价值：1百万美元 * 0.0009 = 900美元

In this case, if the cost of improving availability by one nine is less than $900, it is worth the investment. If the cost is greater than $900, the costs will exceed the projected increase in revenue.

在这种情况下，如果将可用性提高一个数量级的成本低于900美元，那么这个投资是值得的。如果成本高于900美元，则成本将超过预期的收入增长。

It may be harder to set these targets when we do not have a simple translation function between reliability and revenue. One useful strategy may be to consider the background error rate of ISPs on the Internet. If failures are being measured from the end-user perspective and it is possible to drive the error rate for the service below the background error rate, those errors will fall within the noise for a given user’s Internet connection. While there are significant differences between ISPs and protocols (e.g., TCP versus UDP, IPv4 versus IPv6), we’ve measured the typical background error rate for ISPs as falling between 0.01% and 1%.

当我们没有一个简单的可靠性和收入转换函数时，设定这些目标可能会更加困难。一个有用的策略可能是考虑互联网服务提供商的背景错误率。如果故障是从终端用户的角度进行测量的，并且可以将服务的错误率降到背景错误率以下，那么这些错误将在给定用户的互联网连接的噪声范围内。虽然ISP和协议（例如TCP与UDP、IPv4与IPv6）之间存在显着差异，但我们测量出ISP的典型背景错误率介于0.01％和1％之间。

<br>

#### **Other service metrics**

#### **其他服务指标**

Examining the risk tolerance of services in relation to metrics besides availability is often fruitful. Understanding which metrics are important and which metrics aren’t important provides us with degrees of freedom when attempting to take thoughtful risks.

在除可用性之外的指标检查服务的风险承受能力通常是有益的。了解哪些指标是重要的，哪些指标不重要，为我们在尝试风险时提供了自由度。

Service latency for our Ads systems provides an illustrative example. When Google first launched Web Search, one of the service’s key distinguishing features was speed. When we introduced AdWords, which displays advertisements next to search results, a key requirement of the system was that the ads should not slow down the search experience. This requirement has driven the engineering goals in each generation of AdWords systems and is treated as an invariant.

我们广告系统的服务延迟为一个说明性的例子。当Google首次推出Web搜索时，该服务的一个关键特点是速度。当我们推出AdWords时，它在搜索结果旁边展示广告，该系统的一个关键要求是广告不应该拖慢搜索体验。这个要求推动了每一代AdWords系统的工程目标，并被视为一个不变量。

AdSense, Google’s ads system that serves contextual ads in response to requests from JavaScript code that publishers insert into their websites, has a very different latency goal. The latency goal for AdSense is to avoid slowing down the rendering of the third-party page when inserting contextual ads. The specific latency target, then, is dependent on the speed at which a given publisher’s page renders. This means that AdSense ads can generally be served hundreds of milliseconds slower than AdWords ads.

AdSense是Google的广告系统，它根据发布者插入到其网站中的JavaScript代码的请求提供上下文广告，其服务延迟目标与AdWords有很大的不同。AdSense的延迟目标是避免在插入上下文广告时减慢第三方页面的呈现速度。具体的延迟目标取决于特定发布者页面的呈现速度。这意味着AdSense广告通常可以比AdWords广告慢数百毫秒提供服务。

This looser serving latency requirement has allowed us to make many smart trade- offs in provisioning (i.e., determining the quantity and locations of serving resources we use), which save us substantial cost over naive provisioning. In other words, given the relative insensitivity of the AdSense service to moderate changes in latency performance, we are able to consolidate serving into fewer geographical locations, reducing our operational overhead.

这种更松散的服务延迟要求使我们能够在供应（即确定我们使用的服务资源的数量和位置）方面做出许多明智的权衡，从而节省了我们大量的成本。换句话说，考虑到AdSense服务对延迟性能的中等变化的相对不敏感性，我们能够将服务集中到较少的地理位置，从而降低了我们的运营开销。

<br>

### **Identifying the Risk Tolerance of Infrastructure Services**

### **确定基础设施服务的风险承受能力**

The requirements for building and running infrastructure components differ from the requirements for consumer products in a number of ways. A fundamental difference is that, by definition, infrastructure components have multiple clients, often with varying needs.

构建和运行基础设施组件的要求与消费者服务的要求在许多方面不同。一个基本的区别是，按定义，基础设施组件有多个客户端，这些客户端通常具有不同的需求。

<br>

#### **Target level of availability**

#### **目标可用性水平**

Consider Bigtable [[Cha06]](https://research.google.com/archive/bigtable.html), a massive-scale distributed storage system for structured data. Some consumer services serve data directly from Bigtable in the path of a user request. Such services need low latency and high reliability. Other teams use Bigtable as a repository for data that they use to perform offline analysis (e.g., MapReduce) on a regular basis. These teams tend to be more concerned about throughput than reliability. Risk tolerance for these two use cases is quite distinct.

考虑 Bigtable [[Cha06]](https://research.google.com/archive/bigtable.html)，这是一个用于结构化数据的大规模分布式存储系统。一些消费者服务会直接从Bigtable中为用户请求提供数据。这些服务需要低延迟和高可靠性。其他团队则将Bigtable用作数据存储库，以便定期执行离线分析（例如MapReduce）。这些团队更关心吞吐量而不是可靠性。对于这两种用例，风险承受能力是非常不同的。

One approach to meeting the needs of both use cases is to engineer all infrastructure services to be ultra-reliable. Given the fact that these infrastructure services also tend to aggregate huge amounts of resources, such an approach is usually far too expensive in practice. To understand the different needs of the different types of users, you can look at the desired state of the request queue for each type of Bigtable user.

满足这两种场景需求的一种方法是将所有基础设施服务都设计为超高可靠性。鉴于这些基础设施服务还倾向于聚合大量资源，这种方法在实践中通常过于昂贵。为了了解不同类型用户的不同需求，可以查看每种Bigtable用户的请求队列的期望状态。

<br>

#### **Types of failures**

#### **故障类型**

The low-latency user wants Bigtable’s request queues to be (almost always) empty so that the system can process each outstanding request immediately upon arrival. (Indeed, inefficient queuing is often a cause of high tail latency.) The user concerned with offline analysis is more interested in system throughput, so that user wants request queues to never be empty. To optimize for throughput, the Bigtable system should never need to idle while waiting for its next request.

低延迟的用户希望Bigtable的请求队列（几乎总是）为空，以便系统可以在每个未完成的请求到达时立即处理它。 （事实上，低效的排队常常是高延迟的原因。）关注离线分析的用户更关心系统吞吐量，因此该用户希望请求队列永远不会为空。为了优化吞吐量，Bigtable系统应该永远不需要闲置等待下一个请求。

As you can see, success and failure are antithetical for these sets of users. Success for the low-latency user is failure for the user concerned with offline analysis.

正如你所看到的，对于这些用户群体来说，成功和失败是相对的。对于低延迟用户来说的成功对于关注离线分析的用户来说则是失败。

<br>

#### **Cost**

#### **成本**

One way to satisfy these competing constraints in a cost-effective manner is to partition the infrastructure and offer it at multiple independent levels of service. In the Bigtable example, we can build two types of clusters: low-latency clusters and throughput clusters. The low-latency clusters are designed to be operated and used by services that need low latency and high reliability. To ensure short queue lengths and satisfy more stringent client isolation requirements, the Bigtable system can be provisioned with a substantial amount of slack capacity for reduced contention and increased redundancy. The throughput clusters, on the other hand, can be provisioned to run very hot and with less redundancy, optimizing throughput over latency. In practice, we are able to satisfy these relaxed needs at a much lower cost, perhaps as little as 10–50% of the cost of a low-latency cluster. Given Bigtable’s massive scale, this cost savings becomes significant very quickly.

以一种经济有效的方式满足这些相互竞争的约束条件的方法之一是对基础设施进行分区并在多个独立的服务级别上提供它。在Bigtable的例子中，我们可以建立两种类型的集群：低延迟集群和吞吐量集群。低延迟集群旨在由需要低延迟和高可靠性的服务运行和使用。为了确保较短的队列长度并满足更严格的客户端隔离要求，Bigtable系统可以配置大量备用容量以减少争用和增加冗余。另一方面，吞吐量集群可以配置为非常高效且冗余较少，优化吞吐量而非延迟。在实践中，我们能够以更低的成本满足这些放松的需求，成本可能只有低延迟集群成本的10-50％。鉴于Bigtable的大规模，这种成本节省非常快速而显著。

The key strategy with regards to infrastructure is to deliver services with explicitly delineated levels of service, thus enabling the clients to make the right risk and cost trade-offs when building their systems. With explicitly delineated levels of service, the infrastructure providers can effectively externalize the difference in the cost it takes to provide service at a given level to clients. Exposing cost in this way motivates the clients to choose the level of service with the lowest cost that still meets their needs. For example, Google+ can decide to put data critical to enforcing user privacy in a high- availability, globally consistent datastore (e.g., a globally replicated SQL-like system like Spanner [[Cor12]](https://research.google.com/archive/spanner.html)), while putting optional data (data that isn’t critical, but that enhances the user experience) in a cheaper, less reliable, less fresh, and eventually consistent datastore (e.g., a NoSQL store with best-effort replication like Bigtable).

关于基础设施的关键策略是提供具有明确定义的服务级别，从而使客户在构建其系统时能够做出正确的风险和成本权衡。通过明确定义的服务级别，基础设施提供商可以有效地将在特定级别提供服务所需成本的差异外部化给客户。以这种方式公开成本可以激励客户选择具有最低成本且仍能满足其需求的服务级别。例如，Google+可以决定将对执行用户隐私的关键数据放置在高可用性、全球一致的数据存储中（例如类似Spanner [[Cor12]](https://research.google.com/archive/spanner.html) 的全球复制SQL系统），而将可选数据（不是关键的数据，但可以增强用户体验）放置在成本更低、可靠性且最终一致的数据存储中（例如像Bigtable这样的具有尽力而为复制的NoSQL存储）。

Note that we can run multiple classes of services using identical hardware and software. We can provide vastly different service guarantees by adjusting a variety of service characteristics, such as the quantities of resources, the degree of redundancy, the geographical provisioning constraints, and, critically, the infrastructure software configuration.

请注意，我们可以使用相同的硬件和软件运行多个服务类别。通过调整各种服务特征，例如资源数量、冗余程度、地理部署限制以及关键的基础设施软件配置，我们可以提供截然不同的服务保证。

<br>

#### **Example: Frontend infrastructure**

#### **例子：前端基础设施**

To demonstrate that these risk-tolerance assessment principles do not just apply to storage infrastructure, let’s look at another large class of service: Google’s frontend infrastructure. The frontend infrastructure consists of reverse proxy and load balancing systems running close to the edge of our network. These are the systems that, among other things, serve as one endpoint of the connections from end users (e.g., terminate TCP from the user’s browser). Given their critical role, we engineer these systems to deliver an extremely high level of reliability. While consumer services can often limit the visibility of unreliability in backends, these infrastructure systems are not so lucky. If a request never makes it to the application service frontend server, it is lost.

为了展示这些风险容忍评估原则不仅适用于存储基础设施，让我们看看另一个大类服务：Google的前端基础设施。前端基础设施包括反向代理和负载均衡系统，运行在我们网络的边缘。这些系统是终端用户连接的其中一个端点（例如，终端用户浏览器的TCP连接），并担负着其他重要任务。考虑到它们的关键作用，我们设计这些系统以提供极高的可靠性。尽管消费者服务通常可以限制后端不可靠性的可见性，但这些基础设施系统并没有这么幸运。如果一个请求从未到达应用程序服务前端服务器，它就丢失了。

We’ve explored the ways to identify the risk tolerance of both consumer and infrastructure services. Now, we’ll discuss using that tolerance level to manage unreliability via error budgets.

我们已经探讨了如何确定消费者和基础设施服务的风险承受能力。现在，我们将讨论如何利用这种容忍度水平通过错误预算来管理不可靠性。

<br>

---

**[Back to contents of the chapter（返回章节目录）](embracing_risk.md)**

* **Previous Section（上一节）：[Measuring Service Risk（衡量服务风险）](measuring_service_risk.md)**
* **Next Section（下一节）：[Motivation for Error Budgets（错误预算）](motivation_for_error_budgets.md)**
