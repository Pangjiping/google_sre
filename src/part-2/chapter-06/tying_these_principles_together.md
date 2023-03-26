## **Tying These Principles Together**

## **将这些原则联系起来**

The principles discussed in this chapter can be tied together into a philosophy on monitoring and alerting that’s widely endorsed and followed within Google SRE teams. While this monitoring philosophy is a bit aspirational, it’s a good starting point for writing or reviewing a new alert, and it can help your organization ask the right questions, regardless of the size of your organization or the complexity of your service or system.

本章所讨论的原则可以被捆绑在一起，成为一个在Google SRE团队中被广泛认可和遵循的监控和警报的理念。虽然这个监控理念有点理想化，但它是编写或审查新警报的一个很好的起点，它可以帮助你的组织提出正确的问题，无论你的组织规模或服务或系统的复杂性如何。

When creating rules for monitoring and alerting, asking the following questions can help you avoid false positives and pager burnout:

* Does this rule detect an otherwise undetected condition that is urgent, actionable, and actively or imminently user-visible?
* Will I ever be able to ignore this alert, knowing it’s benign? When and why will I be able to ignore this alert, and how can I avoid this scenario?
* Does this alert definitely indicate that users are being negatively affected? Are there detectable cases in which users aren’t being negatively impacted, such as drained traffic or test deployments, that should be filtered out?
* Can I take action in response to this alert? Is that action urgent, or could it wait until morning? Could the action be safely automated? Will that action be a long- term fix, or just a short-term workaround?
* Are other people getting paged for this issue, therefore rendering at least one of the pages unnecessary?

在创建监控和警报的规则时，提出以下问题可以帮助你避免虚假警报和呼叫：

* 这条规则是否检测到了一个原本未被检测到的状况，该状况是紧急的、可操作的，并且是积极的或即将被用户看到的？
* 我是否能够忽略这个警报，知道它是良性的？什么时候以及为什么我能够忽略这个警报，以及我如何能够避免这种情况的发生？
* 这个警报是否肯定表明用户受到了负面影响？是否有可检测到的用户没有受到负面影响的情况，如耗尽流量或测试部署，应该被过滤掉？
* 我可以针对这个警报采取行动吗？这个行动是紧急的，还是可以等到早上？该行动是否可以安全地自动化？该行动将是一个长期的修复，还是只是一个短期的变通？
* 其他人是否因为这个问题而被呼叫，因此至少有一个呼叫是不必要的？

These questions reflect a fundamental philosophy on pages and pagers:

* Every time the pager goes off, I should be able to react with a sense of urgency. I can only react with a sense of urgency a few times a day before I become fatigued.
* Every page should be actionable.
* Every page response should require intelligence. If a page merely merits a robotic response, it shouldn’t be a page.
* Pages should be about a novel problem or an event that hasn’t been seen before.

这些问题反映了关于呼叫和传呼机的基本理念：

* 每次传呼机响起，我都应该能够做出紧急反应。我每天只能做出几次紧急反应，然后就会感到疲惫。
* 每个呼叫都应该是可操作的。
* 每个呼叫的回应都应该需要智慧。如果一个呼叫仅仅值得一个机器人的回应，它就不应该是一个呼叫。
* 呼叫应该是关于一个新问题或一个以前没有见过的事件。

Such a perspective dissipates certain distinctions: if a page satisfies the preceding four bullets, it’s irrelevant whether the page is triggered by white-box or black-box monitoring. This perspective also amplifies certain distinctions: it’s better to spend much more effort on catching symptoms than causes; when it comes to causes, only worry about very definite, very imminent causes.

这样的观点消解了某些区别：如果一个呼叫符合前面的四条规定，那么这个呼叫是由白盒还是黑盒监控触发的就无关紧要。这种观点也放大了某些区别：花更多的精力去捕捉问题而不是原因；当涉及到原因时，只需要担心非常明确的、非常紧迫的原因。

<br>

---

**[Back to contents of the chapter（返回章节目录）](monitoring_distributed_systems.md)**

* **Previous Section（上一节）：[As Simple as Possible, No Simpler（尽可能地简单）](as_simple_as_possible.md)**
* **Next Section（下一节）：[Monitoring for the Long Term（长期监控）](monitoring_for_the_long_term.md)**
