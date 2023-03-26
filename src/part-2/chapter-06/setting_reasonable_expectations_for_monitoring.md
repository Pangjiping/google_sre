## **Setting Reasonable Expectations for Monitoring**

## **设定合理的监控期望值**

Monitoring a complex application is a significant engineering endeavor in and of itself. Even with substantial existing infrastructure for instrumentation, collection, display, and alerting in place, a Google SRE team with 10–12 members typically has one or sometimes two members whose primary assignment is to build and maintain monitoring systems for their service. This number has decreased over time as we generalize and centralize common monitoring infrastructure, but every SRE team typically has at least one "monitoring person." (That being said, while it can be fun to have access to traffic graph dashboards and the like, SRE teams carefully avoid any situation that requires someone to "stare at a screen to watch for problems.")

监控一个复杂的应用程序本身就是一项重要的工程工作。即使有大量现有的仪器、收集、显示和警报的基础设施，一个有10-12名成员的GoogleSRE团队通常有一个或两个成员的主要任务是为他们的服务建立和维护监控系统。随着时间的推移，这个数字已经减少，因为我们普及和集中了共同的监控基础设施，但每个SRE团队通常至少有一个“监控人员”。(这就是说，虽然访问流量图表仪表板和类似的东西可能很有趣，但SRE团队小心地避免任何需要有人“盯着屏幕看问题”的情况。)

In general, Google has trended toward simpler and faster monitoring systems, with better tools for post hoc analysis. We avoid "magic" systems that try to learn thresholds or automatically detect causality. Rules that detect unexpected changes in end-user request rates are one counterexample; while these rules are still kept as simple as possible, they give a very quick detection of a very simple, specific, severe anomaly. Other uses of monitoring data such as capacity planning and traffic prediction can tolerate more fragility, and thus, more complexity. Observational experiments conducted over a very long time horizon (months or years) with a low sampling rate (hours or days) can also often tolerate more fragility because occasional missed samples won’t hide a long-running trend.

总的来说，Google的趋势是更简单、更快速的监控系统，有更好的工具进行事后分析。我们避免那些试图学习阈值或自动检测因果关系的“神奇”系统。检测终端用户请求率意外变化的规则是一个反例；虽然这些规则仍然尽可能地保持简单，但它们对一个非常简单、具体、严重的异常情况给予了非常快速的检测。监控数据的其他用途，如容量规划和流量预测，可以容忍更多的脆弱性，因此也更复杂。在很长的时间范围内（数月或数年）进行的观察实验，其采样率较低（数小时或数天），通常也可以容忍更多的脆弱性，因为偶尔错过的样本不会掩盖一个长期运行的趋势。

Google SRE has experienced only limited success with complex dependency hierarchies. We seldom use rules such as, "If I know the database is slow, alert for a slow database; otherwise, alert for the website being generally slow." Dependency-reliant rules usually pertain to very stable parts of our system, such as our system for draining user traffic away from a datacenter. For example, "If a datacenter is drained, then don’t alert me on its latency" is one common datacenter alerting rule. Few teams at Google maintain complex dependency hierarchies because our infrastructure has a steady rate of continuous refactoring.

GoogleSRE在处理复杂的依赖层次结构方面只取得了有限的成功。我们很少使用这样的规则：“如果我知道数据库很慢，就对慢的数据库发出警报；否则，就对网站普遍缓慢发出警报。”依赖关系的规则通常与我们系统中非常稳定的部分有关，比如我们将用户流量从数据中心引出的系统。例如，“如果一个数据中心被耗尽，那么就不要提醒我它的延迟”是一个常见的数据中心警报规则。在Google，很少有团队维护复杂的依赖层次结构，因为我们的基础设施有一个稳定的持续重构率。

Some of the ideas described in this chapter are still aspirational: there is always room to move more rapidly from symptom to root cause(s), especially in ever-changing systems. So while this chapter sets out some goals for monitoring systems, and some ways to achieve these goals, it’s important that monitoring systems—especially the critical path from the onset of a production problem, through a page to a human, through basic triage and deep debugging—be kept simple and comprehensible by everyone on the team.

本章所描述的一些想法仍然是理想的：从症状到根本原因，特别是在不断变化的系统中，总是有更快发展的空间。因此，尽管本章提出了监控系统的一些目标，以及实现这些目标的一些方法，但重要的是，监控系统--特别是从生产问题的开始，通过一个呼叫到一个人，通过基本的分流和深度调试的关键路径--要保持简单，并让团队的每个人都能理解。

Similarly, to keep noise low and signal high, the elements of your monitoring system that direct to a pager need to be very simple and robust. Rules that generate alerts for humans should be simple to understand and represent a clear failure.

同样地，为了保持低噪音，你的监控系统中指向呼叫器的元素需要非常简单和强大。为人类产生警报的规则应该是简单易懂的，并代表一个明确的故障。

<br>

---

**[Back to contents of the chapter（返回章节目录）](monitoring_distributed_systems.md)**

* **Previous Section（上一节）：[Why Monitor?（为什么要监控）](why_monitor.md)**
* **Next Section（下一节）：[Symptoms Versus Causes（症状与原因）](symptoms_versus_causes.md)**
