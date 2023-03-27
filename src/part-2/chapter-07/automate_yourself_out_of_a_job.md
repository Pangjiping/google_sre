## **Automate Yourself Out of a Job: Automate ALL the Things!**

## **让自己的工作自动化：把所有的事情都自动化!**

For a long while, the Ads products at Google stored their data in a MySQL database. Because Ads data obviously has high reliability requirements, an SRE team was charged with looking after that infrastructure. From 2005 to 2008, the Ads Database mostly ran in what we considered to be a mature and managed state. For example, we had automated away the worst, but not all, of the routine work for standard replica replacements. We believed the Ads Database was well managed and that we had harvested most of the low-hanging fruit in terms of optimization and scale. However, as daily operations became comfortable, team members began to look at the next level of system development: migrating MySQL onto Google’s cluster scheduling system, Borg.

在很长一段时间里，Google的广告产品将其数据存储在MySQL数据库中。因为广告数据显然有很高的可靠性要求，一个SRE团队负责管理这个基础设施。从2005年到2008年，Ads数据库大多运行在我们认为是可靠的状态。例如，我们已经自动化了最糟糕的，但不是所有的，标准复制替换的常规工作。我们认为广告数据库管理良好，在优化和规模方面，我们已经收获了大部分的成果。然而，随着日常运维任务增多，团队成员开始关注系统发展的下一个层次：将MySQL迁移到Google的集群调度系统Borg上。

We hoped this migration would provide two main benefits:

* Completely eliminate machine/replica maintenance: Borg would automatically handle the setup/restart of new and broken tasks.
* Enable bin-packing of multiple MySQL instances on the same physical machine: Borg would enable more efficient use of machine resources via Containers.

我们希望这种迁移能带来两个主要好处：

* 完全消除机器/副本的维护：Borg将自动处理新的和坏的任务的设置/重新启动。
* 启用同一台物理机器上的多个MySQL实例的bin-packing：Borg将通过容器使机器资源得到更有效的利用。

In late 2008, we successfully deployed a proof of concept MySQL instance on Borg. Unfortunately, this was accompanied by a significant new difficulty. A core operating characteristic of Borg is that its tasks move around automatically. Tasks commonly move within Borg as frequently as once or twice per week. This frequency was tolerable for our database replicas, but unacceptable for our masters.

在2008年底，我们成功地在Borg上部署了一个概念验证的MySQL实例。不幸的是，这伴随着一个重大的新困难。Borg的一个核心操作特点是其任务会自动移动。任务在Borg中的移动频率通常为每周一到两次。这种频率对我们的数据库副本来说是可以容忍的，但对我们的主站来说是不可接受的。

At that time, the process for master failover took 30–90 minutes per instance. Simply because we ran on shared machines and were subject to reboots for kernel upgrades, in addition to the normal rate of machine failure, we had to expect a number of otherwise unrelated failovers every week. This factor, in combination with the number of shards on which our system was hosted, meant that:

* Manual failovers would consume a substantial amount of human hours and would give us best-case availability of 99% uptime, which fell short of the actual business requirements of the product.
* In order to meet our error budgets, each failover would have to take less than 30 seconds of downtime. There was no way to optimize a human-dependent procedure to make downtime shorter than 30 seconds.

当时，每个实例的主站故障切换过程需要30-90分钟。仅仅因为我们在共享机器上运行，并且要为内核升级而重启，除了正常的机器故障率之外，我们不得不期待每周有一些本来不相关的故障切换。这个因素，再加上我们系统所在的分片的数量，意味着：

* 人工故障切换将消耗大量的人力时间，并使我们的最佳可用性达到99%的正常运行时间，这与产品的实际业务要求不符。
* 为了满足我们的错误预算，每次故障转移必须花费少于30秒的停机时间。我们没有办法优化一个依赖人类的程序，使停机时间短于30秒。

Therefore, our only choice was to automate failover. Actually, we needed to automate more than just failover.

因此，我们唯一的选择是自动进行故障切换。事实上，我们需要自动化的不仅仅是故障转移。

In 2009 Ads SRE completed our automated failover daemon, which we dubbed "Decider." Decider could complete MySQL failovers for both planned and unplanned failovers in less than 30 seconds 95% of the time. With the creation of Decider, MySQL on Borg (MoB) finally became a reality. We graduated from optimizing our infrastructure for a lack of failover to embracing the idea that failure is inevitable, and therefore optimizing to recover quickly through automation.

2009年，Ads SRE完成了我们的自动故障转移守护程序，我们称之为“Decider”。Decider可以在95%的时间内完成MySQL计划内和计划外的故障转移，时间不超过30秒。随着Decider的诞生，MySQL on Borg（MoB）终于成为了现实。我们从为缺乏故障转移而优化我们的基础设施，到接受故障是不可避免的想法，因此通过自动化优化来快速恢复。

While automation let us achieve highly available MySQL in a world that forced up to two restarts per week, it did come with its own set of costs. All of our applications had to be changed to include significantly more failure-handling logic than before. Given that the norm in the MySQL development world is to assume that the MySQL instance will be the most stable component in the stack, this switch meant customizing software like JDBC to be more tolerant of our failure-prone environment. However, the benefits of migrating to MoB with Decider were well worth these costs. Once on MoB, the time our team spent on mundane operational tasks dropped by 95%. Our failovers were automated, so an outage of a single database task no longer paged a human.

虽然自动化让我们在一个每周被迫重启两次的世界中实现了MySQL的高度可用，但它确实带来了自己的一系列成本。我们所有的应用程序都必须改变，以包括比以前多得多的故障处理逻辑。鉴于MySQL开发领域的规范是假设MySQL实例将是堆栈中最稳定的组件，这种转换意味着定制JDBC等软件，以便对我们易发生故障的环境有更大的容忍度。然而，通过Decider迁移到MoB的好处是非常值得这些成本的。一旦使用MoB，我们的团队花在运维任务上的时间减少了95%。我们的故障转移是自动化的，所以一个单一的数据库任务的中断不再需要人去处理。

The main upshot of this new automation was that we had a lot more free time to spend on improving other parts of the infrastructure. Such improvements had a cascading effect: the more time we saved, the more time we were able to spend on optimizing and automating other tedious work. Eventually, we were able to automate schema changes, causing the cost of total operational maintenance of the Ads Database to drop by nearly 95%. Some might say that we had successfully automated ourselves out of this job. The hardware side of our domain also saw improvement. Migrating to MoB freed up considerable resources because we could schedule multiple MySQL instances on the same machines, which improved utilization of our hardware. In total, we were able to free up about 60% of our hardware. Our team was now flush with hardware and engineering resources.

这种新的自动化的主要结果是，我们有更多的自由时间用于改善基础设施的其他部分。这种改进有一个连带效应：我们节省的时间越多，我们就能有更多的时间用于优化和自动化其他繁琐的工作。最终，我们能够实现模式变更的自动化，使广告数据库的总运维成本下降了近95%。有人可能会说，我们已经成功地将自己从这项工作中自动化了。我们的硬件方面也得到了改善。迁移到MoB释放了相当多的资源，因为我们可以在同一台机器上部署多个MySQL实例，这提高了我们硬件的利用率。总的来说，我们能够释放出大约60%的硬件。我们的团队现在在硬件和工程资源方面都很充裕。

This example demonstrates the wisdom of going the extra mile to deliver a platform rather than replacing existing manual procedures. The next example comes from the cluster infrastructure group, and illustrates some of the more difficult trade-offs you might encounter on your way to automating all the things.

这个例子说明了多走一步路来提供一个平台的智慧，而不是取代现有的手工程序。下一个例子来自于集群基础设施，它说明了你在实现所有事情自动化的道路上可能遇到的一些比较困难的权衡。

<br>

---

**[Back to contents of the chapter（返回章节目录）](the_evolution_of_automation_at_google.md)**

* **Previous Section（上一节）：[The Use Cases for Automation（使用自动化的例子）](the_use_cases_for_automation.md)**
* **Next Section（下一节）：[Soothing the Pain: Applying Automation to Cluster Turnups（舒缓痛苦：将自动化应用于集群启动）](soothing_the_pain.md)**
