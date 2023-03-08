## **Managing Risk**

## **管理风险**

Unreliable systems can quickly erode users’ confidence, so we want to reduce the chance of system failure. However, experience shows that as we build systems, cost does not increase linearly as reliability increments—an incremental improvement in reliability may cost 100x more than the previous increment. The costliness has two dimensions:

The cost of redundant machine/compute resources: The cost associated with redundant equipment that, for example, allows us to take systems offline for routine or unforeseen maintenance, or provides space for us to store parity code blocks that provide a minimum data durability guarantee.

The opportunity cost: The cost borne by an organization when it allocates engineering resources to build systems or features that diminish risk instead of features that are directly visible to or usable by end users. These engineers no longer work on new features and products for end users.

不可靠的系统很快就会破坏用户的信心，因此我们希望降低系统故障的机率。然而，经验表明，随着我们构建系统，成本并不会像可靠性增量那样线性增加——可靠性的逐步提高可能比上一个增量的成本高100倍。成本昂贵有两个方面：

冗余机器/计算资源的成本：这是与冗余设备相关的成本，例如，它使我们能够将系统脱机进行常规或意外维护，或提供空间来存储提供最小数据耐久性保证的奇偶校验码块。

机会成本：组织承担的成本，当其分配工程资源来构建降低风险的系统或功能，而不是直接面向最终用户可见或可用的功能。这些工程师不再致力于为最终用户开发新功能和产品。

In SRE, we manage service reliability largely by managing risk. We conceptualize risk as a continuum. We give equal importance to figuring out how to engineer greater reliability into Google systems and identifying the appropriate level of tolerance for the services we run. Doing so allows us to perform a cost/benefit analysis to determine, for example, where on the (nonlinear) risk continuum we should place Search, Ads, Gmail, or Photos. Our goal is to explicitly align the risk taken by a given service with the risk the business is willing to bear. We strive to make a service reliable enough, but no more reliable than it needs to be. That is, when we set an availability target of 99.99%,we want to exceed it, but not by much: that would waste opportunities to add features to the system, clean up technical debt, or reduce its operational costs. In a sense, we view the availability target as both a minimum and a maximum. The key advantage of this framing is that it unlocks explicit, thoughtful risktaking.

在SRE中，我们通过管理风险来管理服务的可靠性。我们将风险看作是一个连续的概念。我们重视找出如何将更大的可靠性工程化到Google系统中，并确定我们运行的服务的适当的容错级别。这样做可以让我们进行成本/效益分析，以确定搜索、广告、Gmail或Photos应该在哪个（非线性的）风险连续体上。我们的目标是明确地将一个给定服务所承担的风险与企业愿意承担的风险相匹配。我们努力使一个服务足够可靠，但不要过于可靠。也就是说，当我们设定一个可用性目标为99.99%时，我们希望超过这个目标，但不要过多：这将浪费增加系统功能、清理技术债务或减少其运维成本的机会。从某种意义上说，我们将可用性目标视为最低和最高限制。这种框架的关键优势在于它可以解锁明确、周到的风险承担。

<br>

---

**[Back to contents of the chapter（返回章节目录）](embracing_risk.md)**

* **Next Section（下一节）：[Measuring Service Riske（衡量服务风险）](measuring_service_risk.md)**
