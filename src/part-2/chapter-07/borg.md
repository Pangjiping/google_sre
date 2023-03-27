## **Borg: Birth of the Warehouse-Scale Computer**

## **Borg：仓库级计算机的诞生**

Another way to understand the development of our attitude toward automation, and when and where that automation is best deployed, is to consider the history of the development of our cluster management systems. Like MySQL on Borg, which demonstrated the success of converting manual operations to automatic ones, and the cluster turnup process, which demonstrated the downside of not thinking carefully enough about where and how automation was implemented, developing cluster management also ended up demonstrating another lesson about how automation should be done. Like our previous two examples, something quite sophisticated was created as the eventual result of continuous evolution from simpler beginnings.

另一种理解我们对自动化态度的发展，以及何时何地最适合部署自动化的方法是考虑我们的集群管理系统的发展历史。就像MySQL在Borg上展示了将手工操作转换为自动操作的成功，以及集群启动过程展示了对自动化的地点和方式考虑不够周全的弊端，发展集群管理也最终展示了关于如何实现自动化的另一个教训。就像我们之前的两个例子一样，一些相当复杂的东西是作为从简单的开始不断演变的最终结果而产生的。

Google’s clusters were initially deployed much like everyone else’s small networks of the time: racks of machines with specific purposes and heterogeneous configurations. Engineers would log in to some well-known "master" machine to perform administrative tasks; "golden" binaries and configuration lived on these masters. As we had only one colo provider, most naming logic implicitly assumed that location. As production grew, and we began to use multiple clusters, different domains (cluster names) entered the picture. It became necessary to have a file describing what each machine did, which grouped machines under some loose naming strategy. This descriptor file, in combination with the equivalent of a parallel SSH, allowed us to reboot (for example) all the search machines in one go. Around this time, it was common to get tickets like "search is done with machine x1, crawl can have the machine now."

Google的集群最初的部署很像当时的小型网络：具有特定目标和异构配置的机器机架。工程师们会登录到一些“主”机上执行管理任务；二进制文件和配置都在这些主机上。由于我们只有一个主机供应商，大多数命名逻辑都隐含了这个位置。随着生产的增长，我们开始使用多个集群，不同的域（集群名称）接入管理。因此，有必要建立一个文件，描述每台机器的作用，并根据一些松散的命名策略对机器进行分组。这个描述符文件，结合相当于一个平行的SSH，使我们能够一次性重新启动所有的搜索机器。大约在这个时候，经常会收到这样的通知：“机器x1的搜索工作已经完成，现在可以爬到机器上了。”

Automation development began. Initially automation consisted of simple Python scripts for operations such as the following:

* Service management: keeping services running (e.g., restarts after segfaults)
* Tracking what services were supposed to run on which machines
* Log message parsing: SSHing into each machine and looking for regexps

自动化开发开始了。最初的自动化由简单的Python脚本组成，用于以下操作：

* 服务管理：保持服务运行（例如，在segfaults之后重新启动）
* 跟踪哪些服务应该在哪些机器上运行
* 日志信息解析：SSH进入每台机器，通过正则表达式查找日志

Automation eventually mutated into a proper database that tracked machine state, and also incorporated more sophisticated monitoring tools. With the union set of the automation available, we could now automatically manage much of the lifecycle of machines: noticing when machines were broken, removing the services, sending them to repair, and restoring the configuration when they came back from repair.

自动化最终演变成了一个适当的数据库，跟踪机器的状态，并且还纳入了更复杂的监控工具。有了可用的自动化联盟，我们现在可以自动管理机器的大部分生命周期：注意到机器的故障，移除服务，将它们送去维修，并在它们维修回来后恢复配置。

But to take a step back, this automation was useful yet profoundly limited, due to the fact that abstractions of the system were relentlessly tied to physical machines. We needed a new approach, hence Borg [Ver15] was born: a system that moved away from the relatively static host/port/job assignments of the previous world, toward treating a collection of machines as a managed sea of resources. Central to its success —and its conception—was the notion of turning cluster management into an entity for which API calls could be issued, to some central coordinator. This liberated extra dimensions of efficiency, flexibility, and reliability: unlike the previous model of machine "ownership," Borg could allow machines to schedule, for example, batch and user-facing tasks on the same machine.

这种自动化是有用的，但也有很大的局限性，因为系统的抽象是无情地与物理机器联系在一起的事实。我们需要一种新的方法，因此Borg[Ver15]诞生了：这个系统摆脱了以前相对静态的主机/端口/工作分配，将机器的集合视为一个管理的资源池。它的成功和它的概念的核心是把集群管理变成一个实体，可以向一些中央协调者发出API调用。这释放了效率、灵活性和可靠性的额外维度：与以前的机器“所有权”模式不同，Borg可以允许机器编排，例如，在同一台机器上的批处理和面向用户的任务。

This functionality ultimately resulted in continuous and automatic operating system upgrades with a very small amount of constant effort—effort that does not scale with the total size of production deployments. Slight deviations in machine state are now automatically fixed; brokenness and lifecycle management are essentially no-ops for SRE at this point. Thousands of machines are born, die, and go into repairs daily with no SRE effort. To echo the words of Ben Treynor Sloss: by taking the approach that this was a software problem, the initial automation bought us enough time to turn cluster management into something autonomous, as opposed to automated. We achieved this goal by bringing ideas related to data distribution, APIs, hub-and-spoke architectures, and classic distributed system software development to bear upon the domain of infrastructure management.

这最终导致了连续和自动的操作系统升级，只需要非常小的努力--这种努力并不随着生产部署的总规模而扩展。现在，机器状态的轻微偏差会被自动修复；在这一点上，故障和生命周期管理对SRE来说基本上是没有问题的。成千上万的机器每天在没有SRE努力的情况下诞生、死亡和进入维修状态。呼应Ben Treynor Sloss的话：通过采取这是一个软件问题的方法，最初的自动化为我们赢得了足够的时间，把集群管理变成自主的东西，而不是自动化。我们通过将与数据分布、API、枢纽和架构以及经典的分布式系统软件开发相关的想法带到基础设施管理领域来实现这一目标。

An interesting analogy is possible here: we can make a direct mapping between the single machine case and the development of cluster management abstractions. In this view, rescheduling on another machine looks a lot like a process moving from one CPU to another: of course, those compute resources happen to be at the other end of a network link, but to what extent does that actually matter? Thinking in these terms, rescheduling looks like an intrinsic feature of the system rather than something one would "automate"—humans couldn’t react fast enough anyway. Similarly in the case of cluster turnup: in this metaphor, cluster turnup is simply additional schedulable capacity, a bit like adding disk or RAM to a single computer. However, a single-node computer is not, in general, expected to continue operating when a large number of components fail. The global computer is—it must be self-repairing to operate once it grows past a certain size, due to the essentially statistically guaranteed large number of failures taking place every second. This implies that as we move systems up the hierarchy from manually triggered, to automatically triggered, to autonomous, some capacity for self-introspection is necessary to survive.

这里可以做一个有趣的类比：我们可以在单机的情况和集群管理抽象的发展之间做一个直接的映射。在这种观点中，在另一台机器上重新安排时间看起来很像一个进程从一个CPU移动到另一个CPU：当然，这些计算资源碰巧在网络链接的另一端，但这实际上有多大的关系呢？从这些方面考虑，重新安排看起来是系统的一个内在特征，而不是人们要“自动化”的东西--人类无论如何都不可能做出足够快的反应。类似的还有集群的启动：在这个比喻中，集群的启动只是额外的可调度能力，有点像在一台电脑上增加磁盘或内存。然而，一般来说，当大量的组件发生故障时，单节点计算机是不会继续运行的。全局计算机则是--一旦它增长到一定的规模，就必须进行自我修复才能运行，因为从统计学上来说，每秒钟都会有大量的故障发生。这意味着，当我们把系统从手动触发的层次上移到自动触发的层次上，再移到自主的层次上，一些自我检查的能力是必需的。

<br>

---

**[Back to contents of the chapter（返回章节目录）](the_evolution_of_automation_at_google.md)**

* **Previous Section（上一节）：[Soothing the Pain: Applying Automation to Cluster Turnups（舒缓痛苦：将自动化应用于集群启动）](soothing_the_pain.md)**
* **Next Section（下一节）：[Reliability Is the Fundamental Feature（可靠性是最基本的特征）](reliability_is_the_fundamental_feature.md)**
