## **Definitions**

## **定义**

There’s no uniformly shared vocabulary for discussing all topics related to monitoring. Even within Google, usage of the following terms varies, but the most common interpretations are listed here.

在讨论与监控有关的话题时，没有统一的词汇。即使在Google内部，以下术语的用法也不尽相同，但这里列出了最常见的解释。

* **Monitoring**. Collecting, processing, aggregating, and displaying real-time quantitative data about a system, such as query counts and types, error counts and types, processing times, and server lifetimes.
* **White-box monitoring**. Monitoring based on metrics exposed by the internals of the system, including logs, interfaces like the Java Virtual Machine Profiling Interface, or an HTTP handler that emits internal statistics.
* **Black-box monitoring**. Testing externally visible behavior as a user would see it.
* **Dashboard**. An application (usually web-based) that provides a summary view of a service’s core metrics. A dashboard may have filters, selectors, and so on, but is prebuilt to expose the metrics most important to its users. The dashboard might also display team information such as ticket queue length, a list of high-priority bugs, the current on-call engineer for a given area of responsibility, or recent pushes.
* **Alert**. A notification intended to be read by a human and that is pushed to a system such as a bug or ticket queue, an email alias, or a pager. Respectively, these alerts are classified as tickets, email alerts, and pages.
* **Root cause**. A defect in a software or human system that, if repaired, instills confidence that this event won’t happen again in the same way. A given incident might have multiple root causes: for example, perhaps it was caused by a combination of insufficient process automation, software that crashed on bogus input, and insufficient testing of the script used to generate the configuration. Each of these factors might stand alone as a root cause, and each should be repaired.
* **Node and machine**. Used interchangeably to indicate a single instance of a running kernel in either a physical server, virtual machine, or container. There might be multiple services worth monitoring on a single machine. The services may either be:
  * Related to each other: for example, a caching server and a web server
  * Unrelated services sharing hardware: for example, a code repository and a master for a configuration system like Puppet or Chef
* **Push**. Any change to a service’s running software or its configuration.

* **监控**。收集、处理、汇总和显示系统的实时定量数据，如查询次数和类型、错误次数和类型、处理时间和服务器寿命。
* **白盒监控**。基于系统内部暴露的指标进行监控，包括日志、像JVM剖析接口这样的接口，或者是发送内部统计数据的HTTP处理器。
* **黑盒监控**。测试外部可见的行为，就像用户看到的那样。
* **仪表板**。一个应用程序（通常是基于网络的），提供一个服务的核心指标的摘要视图。仪表盘可能有过滤器、选择器等，但它是预先建立的，以暴露对其用户最重要的指标。仪表盘还可以显示团队信息，如票据队列长度、高优先级的bug列表、特定责任区的当前待命工程师，或最近的推送。
* **警报**。一个打算由人阅读的通知，它被推送到一个系统，如一个错误或票据队列，一个电子邮件别名，或一个呼叫器。分别来说，这些警报被分为票据、电子邮件警报和呼叫。
* **根本原因**。软件或人类系统中的缺陷，如果得到修复，可以使人相信这一事件不会再以同样的方式发生。一个特定的事件可能有多个根本原因：例如，也许它是由过程自动化不足、软件在虚假输入时崩溃以及对用于生成配置的脚本测试不足等因素共同造成的。这些因素中的每一个都可能单独成为根本原因，并且每一个都应该被修复。
* **节点和机器**。可互换使用，表示物理服务器、虚拟机或容器中运行内核的单一实例。一台机器上可能有多个值得监控的服务。这些服务可以是：
  * 彼此相关：例如，一个缓存服务器和一个网络服务器
  * 不相关的服务共享硬件：例如，代码库和配置系统（如Puppet或Chef）的主机
* **推送**。对一个服务的运行软件或其配置的任何改变。

<br>

---

**[Back to contents of the chapter（返回章节目录）](monitoring_distributed_systems.md)**

* **Next Section（下一节）：[Why Monitor?（为什么要监控）](why_monitor.md)**
