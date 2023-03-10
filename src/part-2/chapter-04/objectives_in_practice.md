## **Objectives in Practice**

## **实践中的SLO**

Start by thinking about (or finding out!) what your users care about, not what you can measure. Often, what your users care about is difficult or impossible to measure, so you’ll end up approximating users’ needs in some way. However, if you simply start with what’s easy to measure, you’ll end up with less useful SLOs. As a result, we’ve sometimes found that working from desired objectives backward to specific indicators works better than choosing indicators and then coming up with targets.

从思考（或发现！）你的用户关心什么开始，而不是你能测量什么。通常情况下，你的用户所关心的东西很难或不可能测量，所以你最终会以某种方式接近用户的需求。然而，如果你只是简单地从容易测量的东西开始，你最终会得到不太有用的SLO。因此，我们有时会发现，从理想的目标向后延伸到具体的指标，比选择指标然后再提出目标要好。

<br>

### **Defining Objectives**

### **确定目标**

For maximum clarity, SLOs should specify how they’re measured and the conditions under which they’re valid. For instance, we might say the following (the second line is the same as the first, but relies on the SLI defaults of the previous section to remove redundancy):

* 99% (averaged over 1 minute) of Get RPC calls will complete in less than 100 ms (measured across all the backend servers).
* 99% of Get RPC calls will complete in less than 100 ms.

为了达到最大的清晰度，SLO应该明确说明它们是如何测量的，以及它们在什么条件下有效。例如，我们可以这样说（第二条与第一条相同，但依靠上一节的SLI默认值来消除冗余）。

* 99%（1分钟内的平均数）的Get RPC调用将在100毫秒内完成（在所有后端服务器上测量）。
* 99%的Get RPC调用将在100毫秒内完成。

If the shape of the performance curves are important, then you can specify multiple SLO targets:

* 90% of Get RPC calls will complete in less than 1 ms.
* 99% of Get RPC calls will complete in less than 10 ms.
* 99.9% of Get RPC calls will complete in less than 100 ms.

如果性能很重要，那么你可以指定多个SLO目标：

* 90%的Get RPC调用将在1毫秒内完成。
* 99%的Get RPC调用将在10毫秒内完成。
* 99.9%的Get RPC调用将在100毫秒内完成。

If you have users with heterogeneous workloads such as a bulk processing pipeline that cares about throughput and an interactive client that cares about latency, it may be appropriate to define separate objectives for each class of workload:

* 95% of throughput clients’ Get RPC calls will complete in < 1 s.
* 99% of latency clients’ Get RPC calls with payloads < 1 kB will complete in < 10ms.

如果你的用户有异构的工作负载，如一个关心吞吐量的批量处理流水线和一个关心延迟的交互式客户端，为每一类工作负载定义单独的目标可能是合适的：

* 95%的吞吐量客户的Get RPC调用将在1s内完成。
* 99%的延迟客户的Get RPC调用的有效载荷<1kB将在10ms内完成。
  
It’s both unrealistic and undesirable to insist that SLOs will be met 100% of the time: doing so can reduce the rate of innovation and deployment, require expensive, overly conservative solutions, or both. Instead, it is better to allow an error budget—a rate at which the SLOs can be missed—and track that on a daily or weekly basis. Upper management will probably want a monthly or quarterly assessment, too. (An error budget is just an SLO for meeting other SLOs!)

坚持认为SLO会在100%的时间内得到满足是不现实的，也是不可取的：这样做会降低创新和部署的速度，需要昂贵的、过于保守的解决方案，或者两者都是。相反，更好的做法是允许一个错误预算--SLO可能被错过的比率--并每天或每周跟踪它。上层管理部门可能也会希望每月或每季度进行一次评估。（错误预算只是满足其他SLO的一个SLO！）。

The rate at which SLOs are missed is a useful indicator for the user-perceived health of the service. It is helpful to track SLOs (and SLO violations) on a daily or weekly basis to see trends and get early warning of potential problems before they happen. Upper management will probably want a monthly or quarterly assessment, too.

错过SLO的比率是一个有用的指标，表明用户认为的服务健康状况。每天或每周跟踪SLO（和违反SLO的情况）是很有帮助的，可以看到趋势并在潜在问题发生之前得到早期警告。上层管理部门可能也会希望每月或每季度进行一次评估。

The SLO violation rate can be compared against the error budget (see ["Motivation for Error Budgets"](./../chapter-03/motivation_for_error_budgets.md) on page 33), with the gap used as an input to the process that decides when to roll out new releases.

SLO违反率可以与错误预算进行比较（见[“错误预算”](./../chapter-03/motivation_for_error_budgets.md)），差距可以作为决定何时推出新版本的过程的输入。

<br>

### **Choosing Targets**

### **选择目标**

Choosing targets (SLOs) is not a purely technical activity because of the product and business implications, which should be reflected in both the SLIs and SLOs (and maybe SLAs) that are selected. Similarly, it may be necessary to trade off certain product attributes against others within the constraints posed by staffing, time to market, hardware availability, and funding. While SRE should be part of this conversation, and advise on the risks and viability of different options, we’ve learned a few lessons that can help make this a more productive discussion:

* Don’t pick a target based on current performance. While understanding the merits and limits of a system is essential, adopting values without reflection may lock you into supporting a system that requires heroic efforts to meet its targets, and that cannot be improved without significant redesign.
* Keep it simple. Complicated aggregations in SLIs can obscure changes to system performance, and are also harder to reason about.
* Avoid absolutes. While it’s tempting to ask for a system that can scale its load "infinitely" without any latency increase and that is "always" available, this requirement is unrealistic. Even a system that approaches such ideals will probably take a long time to design and build, and will be expensive to operate—and probably turn out to be unnecessarily better than what users would be happy (or even delighted) to have.
* Have as few SLOs as possible. Choose just enough SLOs to provide good coverage of your system’s attributes. Defend the SLOs you pick: if you can’t ever win a conversation about priorities by quoting a particular SLO, it’s probably not worth having that SLO.2 However, not all product attributes are amenable to SLOs: it’s hard to specify "user delight" with an SLO.
* Perfection can wait. You can always refine SLO definitions and targets over time as you learn about a system’s behavior. It’s better to start with a loose target that you tighten than to choose an overly strict target that has to be relaxed when you discover it’s unattainable.

选择目标（SLO）并不是一项纯粹的技术活动，因为它涉及到产品和业务，这应该反映在所选择的SLI和SLO（也许还有SLA）中。同样，在人员配置、上市时间、硬件可用性和资金的限制下，可能有必要将某些产品属性与其他属性进行交换。虽然SRE应该是这个对话的一部分，并对不同选项的风险和可行性提出建议，但我们已经学到了一些经验，可以帮助使这个讨论更有成效：

* 不要根据目前的表现来选择目标。虽然了解一个系统的优点和局限性是至关重要的，但不加反思地采用价值观可能会锁定你支持一个需要努力才能达到目标的系统，而这个系统不经过重大的重新设计就无法改进。
* 保持简单。SLI中复杂的汇总可能会掩盖系统性能的变化，而且也更难推理。
* 避免绝对化。虽然要求一个可以“无限”扩展其负载而不增加任何延迟，并且“永远”可用的系统很诱人，但这种要求是不现实的。即使是一个接近这种理想的系统，也可能需要很长的时间来设计和建造，而且运营成本很高--而且可能会变成比用户乐意（甚至高兴）拥有的更好的东西。
* 尽可能少的SLO。选择足够多的SLO来为你的系统的属性提供良好的覆盖。为你选择的SLO辩护：如果你不能通过引用一个特定的SLO来赢得关于优先级的对话，那么它可能不值得拥有这个SLO。
* 完美可以等待。随着时间的推移，你可以不断完善SLO的定义和目标，因为你了解了系统的行为。与其选择一个过于严格的目标，当你发现它无法实现时不得不放松，不如从一个宽松的目标开始，然后收紧。

SLOs can—and should—be a major driver in prioritizing work for SREs and product developers, because they reflect what users care about. A good SLO is a helpful, legitimate forcing function for a development team. But a poorly thought-out SLO can result in wasted work if a team uses heroic efforts to meet an overly aggressive SLO, or a bad product if the SLO is too lax. SLOs are a massive lever: use them wisely.

SLO可以--而且应该--成为SRE和产品开发人员确定工作优先次序的主要驱动力，因为它们反映了用户关心的东西。一个好的SLO对于一个开发团队来说是一个有用的、合法的强制功能。但是，如果一个团队为了达到一个过于激进的SLO而做出英雄般的努力，一个考虑不周的SLO会导致工作的浪费，如果SLO过于宽松，则会导致产品的失败。SLO是一个巨大的杠杆：明智地使用它们。

<br>

### **Control Measures**

### **管控措施**

SLIs and SLOs are crucial elements in the control loops used to manage systems:

1. Monitor and measure the system’s SLIs.
2. Compare the SLIs to the SLOs, and decide whether or not action is needed.
3. If action is needed, figure out what needs to happen in order to meet the target.
4. Take that action.

SLI和SLO是用于管理系统的控制回路中的关键元素：

1. 监测和测量系统的SLI。
2. 将SLI与SLO进行比较，并决定是否需要采取行动。
3. 如果需要采取行动，弄清楚为了达到目标需要发生什么。
4. 采取该行动。

For example, if step 2 shows that request latency is increasing, and will miss the SLO in a few hours unless something is done, step 3 might include testing the hypothesis that the servers are CPU-bound, and deciding to add more of them to spread the load. Without the SLO, you wouldn’t know whether (or when) to take action.

例如，如果第2步显示请求延迟正在增加，并将在几个小时内错过SLO，除非采取一些措施，第3步可能包括测试服务器被CPU占用的假设，并决定增加更多的服务器以分散负载。没有SLO，你就不知道是否（或何时）采取行动。

<br>

### **SLOs Set Expectations**

### **SLO设定期望值**

Publishing SLOs sets expectations for system behavior. Users (and potential users) often want to know what they can expect from a service in order to understand whether it’s appropriate for their use case. For instance, a team wanting to build a photo-sharing website might want to avoid using a service that promises very strong durability and low cost in exchange for slightly lower availability, though the same service might be a perfect fit for an archival records management system.

发布SLO设定了对系统行为的期望。用户（和潜在用户）经常想知道他们能从一个服务中得到什么，以便了解它是否适合他们的使用情况。例如，一个想建立照片共享网站的团队可能想避免使用一个承诺非常强大的持久性和低成本以换取稍低的可用性的服务，尽管同样的服务可能是一个档案记录管理系统的完美选择。

In order to set realistic expectations for your users, you might consider using one or both of the following tactics:

* Keep a safety margin. Using a tighter internal SLO than the SLO advertised to users gives you room to respond to chronic problems before they become visible externally. An SLO buffer also makes it possible to accommodate reimplementations that trade performance for other attributes, such as cost or ease of maintenance, without having to disappoint users.
* Don’t overachieve. Users build on the reality of what you offer, rather than what you say you’ll supply, particularly for infrastructure services. If your service’s actual performance is much better than its stated SLO, users will come to rely on its current performance. You can avoid over-dependence by deliberately taking the system offline occasionally (Google’s Chubby service introduced planned outages in response to being overly available),3 throttling some requests, or designing the system so that it isn’t faster under light loads.

为了给你的用户设定现实的期望，你可以考虑使用以下一种或两种策略：

* 保持一个安全系数。使用比向用户宣传的SLO更严格的内部SLO，使你有空间在慢性问题成为外部可见的问题之前做出反应。一个SLO缓冲区也使你有可能适应以性能换取其他属性的重新实现，例如成本或维护的便利性，而不必让用户失望。
* 不要超额完成任务。用户建立在你所提供的现实上，而不是你说你会提供什么，特别是对于基础设施服务。如果你的服务的实际性能比它所说的SLO好得多，用户就会依赖它目前的性能。你可以通过故意让系统偶尔下线来避免过度依赖（Google的Chubby服务引入了有计划的中断，以应对过高的可用性），对一些请求进行限流，或者设计系统，使其在轻度负载下不会更快。

Understanding how well a system is meeting its expectations helps decide whether to invest in making the system faster, more available, and more resilient. Alternatively, if the service is doing fine, perhaps staff time should be spent on other priorities, such as paying off technical debt, adding new features, or introducing other products.

了解一个系统在多大程度上满足了它的期望，有助于决定是否要投资于使系统更快、更可用、更有弹性。另外，如果服务做得很好，也许员工的时间应该花在其他优先事项上，比如偿还技术债务，增加新的功能，或者引入其他产品。

<br>

---

**[Back to contents of the chapter（返回章节目录）](service_level_objectives.md)**

* **Previous Section（上一节）：[Indicators in Practice（实践中的SLI）](service_level_terminology.md)**
* **Next Section（下一节）：[Agreements in Practice（实践中的SLA）](agreements_in_practice.md)**
