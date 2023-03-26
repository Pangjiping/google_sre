## **Why Monitor?**

## **为什么要监控？**

There are many reasons to monitor a system, including:

* **Analyzing long-term trends**. How big is my database and how fast is it growing? How quickly is my daily- active user count growing?
* **Comparing over time or experiment groups**. Are queries faster with Acme Bucket of Bytes 2.72 versus Ajax DB 3.14? How much better is my memcache hit rate with an extra node? Is my site slower than it was last week?
* **Alerting**. Something is broken, and somebody needs to fix it right now! Or, something might break soon, so somebody should look soon.
* **Building dashboards**. Dashboards should answer basic questions about your service, and normally include some form of the four golden signals (discussed in "The Four Golden Signals" on page 60).
* **Conducting ad hoc retrospective analysis (i.e., debugging)**. Our latency just shot up; what else happened around the same time?

监控一个系统有很多原因，包括：

* **分析长期趋势**。我的数据库有多大，它的增长速度如何？我的日活跃用户数增长有多快？
* **在时间上或实验组上进行比较**。使用Acme Bucket of Bytes 2.72与Ajax DB 3.14的查询速度是否更快？多了一个节点，我的memcache命中率会好多少？我的网站比上周慢吗？
* **警报**。有东西坏了，有人需要马上修理它！或者，有东西可能很快就会坏，所以有人应该尽快查看。或者，有些东西可能很快就会坏掉，所以有人应该尽快查看。
* **建立仪表盘**。仪表板应该回答关于你的服务的基本问题，通常包括四种黄金信号的某种形式（在第60页“四种黄金信号”中讨论）。
* **进行特别的回顾性分析（即调试）**。我们的延迟刚刚飙升；在同一时间还发生了什么？

System monitoring is also helpful in supplying raw input into business analytics and in facilitating analysis of security breaches. Because this book focuses on the engineering domains in which SRE has particular expertise, we won’t discuss these applications of monitoring here.

系统监控也有助于为业务分析提供原始输入，并促进对安全漏洞的分析。因为本书的重点是SRE特别擅长的工程领域，所以我们不会在这里讨论这些监控的应用。

Monitoring and alerting enables a system to tell us when it’s broken, or perhaps to tell us what’s about to break. When the system isn’t able to automatically fix itself, we want a human to investigate the alert, determine if there’s a real problem at hand, mitigate the problem, and determine the root cause of the problem. Unless you’re performing security auditing on very narrowly scoped components of a system, you should never trigger an alert simply because "something seems a bit weird."

监控和警报使一个系统能够告诉我们它什么时候坏了，或者也许告诉我们什么东西要坏了。当系统不能自动修复时，我们希望有一个人去调查警报，确定是否有一个真正的问题，缓解问题，并确定问题的根源。除非你对一个系统中范围很窄的组件进行安全审计，否则你不应该仅仅因为“有些东西看起来有点奇怪”而触发警报。

Paging a human is a quite expensive use of an employee’s time. If an employee is at work, a page interrupts their workflow. If the employee is at home, a page interrupts their personal time, and perhaps even their sleep. When pages occur too frequently, employees second-guess, skim, or even ignore incoming alerts, sometimes even ignoring a "real" page that’s masked by the noise. Outages can be prolonged because other noise interferes with a rapid diagnosis and fix. Effective alerting systems have good signal and very low noise.

呼叫是对员工时间的一种相当昂贵的使用。如果员工在工作中，呼叫会打断他们的工作流程。如果员工在家里，呼叫会打断他们的个人时间，甚至可能打断他们的睡眠。当呼叫出现得太频繁时，员工会略过，甚至忽略传来的警报，有时甚至忽略被噪音掩盖的“真实”呼叫。由于其他噪音干扰了快速诊断和修复，故障可能会被延长。有效的警报系统具有良好的信号和非常低的噪音。

<br>

---

**[Back to contents of the chapter（返回章节目录）](monitoring_distributed_systems.md)**

* **Previous Section（上一节）：[Definitions（定义）](definitions.md)**
* **Next Section（下一节）：[Setting Reasonable Expectations for Monitoring（设定合理的监控期望值）](setting_reasonable_expectations_for_monitoring.md)**
