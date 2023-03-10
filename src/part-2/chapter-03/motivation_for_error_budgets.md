## **Motivation for Error Budgets**

## **错误预算**

Other chapters in this book discuss how tensions can arise between product development teams and SRE teams, given that they are generally evaluated on different metrics. Product development performance is largely evaluated on product velocity, which creates an incentive to push new code as quickly as possible. Meanwhile, SRE performance is (unsurprisingly) evaluated based upon reliability of a service, which implies an incentive to push back against a high rate of change. Information asymmetry between the two teams further amplifies this inherent tension. The product developers have more visibility into the time and effort involved in writing and releasing their code, while the SREs have more visibility into the service’s reliability (and the state of production in general).

本书的其他章节讨论了产品开发团队和SRE团队之间如何产生紧张关系，因为他们通常以不同的指标进行评估。产品开发的表现主要是根据产品的速度来评估的，这就产生了一个激励机制，让他们尽可能快地推出新的代码。同时，SRE的表现是基于服务的可靠性来评估的，这意味着有动力去抵制高速的变化。两个团队之间的信息不对称进一步放大了这种内在的紧张关系。产品开发人员对编写和发布代码的时间和努力有更多的了解，而SRE对服务的可靠性（以及一般的生产状态）有更多的了解。

These tensions often reflect themselves in different opinions about the level of effort that should be put into engineering practices. The following list presents some typical tensions:

Software fault tolerance: How hardened do we make the software to unexpected events? Too little, and we have a brittle, unusable product. Too much, and we have a product no one wants to use (but that runs very stably).

Testing: Again, not enough testing and you have embarrassing outages, privacy data leaks, or a number of other press-worthy events. Too much testing, and you might lose your market.

Push frequency: Every push is risky. How much should we work on reducing that risk, versus doing other work?

Canary duration and size: It’s a best practice to test a new release on some small subset of a typical workload, a practice often called canarying. How long do we wait, and how big is the canary?

这些紧张关系往往反映在对工程实践中应投入的努力程度的不同意见上。下面列出了一些典型的紧张关系。

软件的容错性。我们要让软件对意外事件有多强的承受力？太少了，我们就会有一个脆性的、无法使用的产品。太多了，我们就会有一个没有人愿意使用的产品（但运行非常稳定）。

测试。同样，如果测试不够，你就会出现令人尴尬的故障，隐私数据泄露，或其他一些有新闻价值的事件。测试太多，你可能会失去你的市场。

推送频率。每次推送都有风险。与做其他工作相比，我们应该在多大程度上努力减少这种风险？

金丝雀持续时间和规模。在典型工作负载的一些小子集上测试新版本是一种最佳做法，这种做法通常称为金丝雀测试。我们要等多长时间，金丝雀有多大规模？

Usually, preexisting teams have worked out some kind of informal balance between them as to where the risk/effort boundary lies. Unfortunately, one can rarely prove that this balance is optimal, rather than just a function of the negotiating skills of the engineers involved. Nor should such decisions be driven by politics, fear, or hope. (Indeed, Google SRE’s unofficial motto is “Hope is not a strategy.”) Instead, our goal is to define an objective metric, agreed upon by both sides, that can be used to guide the negotiations in a reproducible way. The more data-based the decision can be, the better.

通常情况下，先前存在的团队已经在这些事之间达成了某种非正式的平衡，即风险/努力的边界在哪里。不幸的是，人们很少能证明这种平衡是最佳的，而不是仅仅是相关工程师的谈判技巧的函数。这种决定也不应该被政治、恐惧或希望所驱动。事实上，谷歌SRE的非官方座右铭是“希望不是一种策略”。相反，我们的目标是定义一个客观的指标，由双方同意，可以用来指导谈判的可复制性。决策越是基于数据，就越好。

<br>

### **Forming Your Error Budget**

### **形成你的错误预算**

In order to base these decisions on objective data, the two teams jointly define a quarterly error budget based on the service’s service level objective, or SLO (see Chapter 4). The error budget provides a clear, objective metric that determines how unreliable the service is allowed to be within a single quarter. This metric removes the politics from negotiations between the SREs and the product developers when deciding how much risk to allow.

为了将这些决定建立在客观数据的基础上，两个团队根据服务水平目标，即SLO（见第四章），共同定义了一个季度错误预算。错误预算提供了一个明确、客观的衡量标准，决定了在一个季度内允许服务有多不可靠。在决定允许多大的风险时，这个指标消除了SRE和产品开发人员之间谈判的政治因素。

Our practice is then as follows:

* Product Management defines an SLO, which sets an expectation of how much uptime the service should have per quarter.
* The actual uptime is measured by a neutral third party: our monitoring system.
* The difference between these two numbers is the “budget” of how much “unreliability” is remaining for the quarter.
* As long as the uptime measured is above the SLO—in other words, as long as there is error budget remaining—new releases can be pushed.

那么我们的做法如下：

* 产品管理部门定义了一个SLO，它设定了服务每季度应该有多少正常运行时间的预期。
* 实际的正常运行时间是由中立的第三方测量的：我们的监测系统。
* 这两个数字之间的差异是“预算”，即该季度还有多少“不可靠”。
* 只要测得的正常运行时间高于SLO--换句话说，只要还有误差预算，就可以推送新版本。

For example, imagine that a service’s SLO is to successfully serve 99.999% of all queries per quarter. This means that the service’s error budget is a failure rate of 0.001% for a given quarter. If a problem causes us to fail 0.0002% of the expected queries for the quarter, the problem spends 20% of the service’s quarterly error budget.

例如，设想一个服务的SLO是每季度成功服务99.999%。这意味着该服务的错误预算是某一季度的失败率为0.001%。如果一个问题导致我们在该季度的预期查询中失败了0.0002%，那么这个问题就花费了该服务季度错误预算的20%。

<br>

### **Benefits**

### **收益**

The main benefit of an error budget is that it provides a common incentive that allows both product development and SRE to focus on finding the right balance between innovation and reliability.

误差预算的主要好处是，它提供了一个共同的激励机制，使产品开发和SRE都能专注于在创新和可靠性之间找到正确的平衡。

Many products use this control loop to manage release velocity: as long as the system’s SLOs are met, releases can continue. If SLO violations occur frequently enough to expend the error budget, releases are temporarily halted while additional resources are invested in system testing and development to make the system more resilient, improve its performance, and so on. More subtle and effective approaches are available than this simple on/off technique:2 for instance, slowing down releases or rolling them back when the SLO-violation error budget is close to being used up.

许多产品使用这种控制循环来管理发布速度：只要系统的SLO得到满足，就可以继续发布。如果违反SLO的情况经常发生，以至于耗费了错误预算，那么就会暂时停止发布，同时在系统测试和开发中投入额外的资源，使系统更有弹性，提高其性能等等。比起这种简单的开/关技术，还有更微妙和有效的方法：例如，当SLO-违反错误预算接近用完时，放慢发布速度或回滚。

For example, if product development wants to skimp on testing or increase push velocity and SRE is resistant, the error budget guides the decision. When the budget is large, the product developers can take more risks. When the budget is nearly drained, the product developers themselves will push for more testing or slower push velocity, as they don’t want to risk using up the budget and stall their launch. In effect, the product development team becomes self-policing. They know the budget and can manage their own risk. (Of course, this outcome relies on an SRE team having the authority to actually stop launches if the SLO is broken.)

例如，如果产品开发想在测试上吝啬，或增加推送速度，而SRE又有阻力，那么错误预算就会指导决策。当预算很大时，产品开发人员可以承担更多的风险。当预算几乎耗尽时，产品开发人员自己会推动更多的测试或更慢的推送速度，因为他们不想冒用预算的风险而拖延他们的发布。实际上，产品开发团队变成了自我监督。他们知道预算，可以管理自己的风险。当然，这个结果取决于SRE团队是否有权力在SLO被破坏的情况下实际停止发布。

What happens if a network outage or datacenter failure reduces the measured SLO? Such events also eat into the error budget. As a result, the number of new pushes may be reduced for the remainder of the quarter. The entire team supports this reduction because everyone shares the responsibility for uptime.

如果网络中断或数据中心故障减少了SLO，会发生什么？此类事件也会消耗错误预算。因此，在本季度的剩余时间里，新推送的数量可能会减少。整个团队都支持这种减少，因为每个人都分担正常运行时间的责任。

The budget also helps to highlight some of the costs of overly high reliability targets, in terms of both inflexibility and slow innovation. If the team is having trouble launching new features, they may elect to loosen the SLO (thus increasing the error budget) in order to increase innovation.

在不灵活和缓慢的创新方面，预算也有助于突出一些过高的可靠性目标的成本。如果团队在推出新功能时遇到困难，他们可以选择放松SLO（从而增加错误预算），以增加创新。

> * Managing service reliability is largely about managing risk, and managing risk can be costly.
> * 100% is probably never the right reliability target: not only is it impossible to achieve, it’s typically more reliability than a service’s users want or notice. Match the profile of the service to the risk the business is willing to take.
> * An error budget aligns incentives and emphasizes joint ownership between SRE and product development. Error budgets make it easier to decide the rate of releases and to effectively defuse discussions about outages with stakeholders, and allows multiple teams to reach the same conclusion about production risk without rancor.

> 管理服务的可靠性在很大程度上就是管理风险，而管理风险的成本很高。
> 100%可能永远不是正确的可靠性目标：它不仅不可能实现，而且通常比服务的用户想要或注意到的可靠性更高。将服务的情况与企业愿意承担的风险相匹配。
> 误差预算使激励机制一致，强调SRE和产品开发之间的共同所有权。错误预算可以更容易地决定发布的速度，并有效地化解与利益相关者关于中断的讨论，并允许多个团队对生产风险达成相同的结论，而不会产生怨恨。

<br>

---

**[Back to contents of the chapter（返回章节目录）](embracing_risk.md)**

* **Previous Section（上一节）：[Risk Tolerance of Services（服务的风险承受能力）](measuring_service_risk.md)**
* **Next Chapter（下一章）：[]()**
