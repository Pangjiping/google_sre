## **The Use Cases for Automation**

## **使用自动化的例子**

In the industry, automation is the term generally used for writing code to solve a wide variety of problems, although the motivations for writing this code, and the solutions themselves, are often quite different. More broadly, in this view, automation is "meta- software"—software to act on software.

在业界，自动化是一般用写代码解决各种问题的术语，尽管写这个代码的动机和解决方案本身往往是相当不同的。更广泛地说，在这种观点中，自动化是“元软件”--软件作用于软件。

As we implied earlier, there are a number of use cases for automation. Here is a non- exhaustive list of examples:

* User account creation
* Cluster turnup and turndown for services
* Software or hardware installation preparation and decommissioning
* Rollouts of new software versions
* Runtime configuration changes
* A special case of runtime config changes: changes to your dependencies

正如我们前面所说明的，有许多自动化的用例。下面是一个非详尽的清单：

* 创建用户账户
* 集群的开启和关闭
* 软件或硬件的安装准备和下线
* 新软件版本的推出
* 运行时配置的改变
* 运行时配置变化的一个特殊情况：对你的依赖关系的变化

This list could continue essentially ad infinitum.

这份清单基本上可以无限地继续下去。

<br>

### **Google SRE’s Use Cases for Automation**

### **Google SRE使用自动化的例子**

In Google, we have all of the use cases just listed, and more.

在Google，我们有刚才列出的所有用例，还有更多。

However, within Google SRE, our primary affinity has typically been for running infrastructure, as opposed to managing the quality of the data that passes over that infrastructure. This line isn’t totally clear—for example, we care deeply if half of a dataset vanishes after a push, and therefore we alert on coarse-grain differences like this, but it’s rare for us to write the equivalent of changing the properties of some arbitrary subset of accounts on a system. Therefore, the context for our automation is often automation to manage the lifecycle of systems, not their data: for example, deployments of a service in a new cluster.

然而，在GoogleSRE中，我们的主要内容通常是运行基础设施，而不是管理通过该基础设施的数据的质量。这条线并不完全清晰--例如，我们非常关心一个数据集在推送后是否有一半消失，因此我们对这样的粗粒度差异发出警报，但我们很少编写相当于改变系统上一些任意的账户子集的属性。因此，我们自动化的背景往往是管理系统生命周期的自动化，而不是它们的数据：例如，在一个新集群中部署服务。

To this extent, SRE’s automation efforts are not far off what many other people and organizations do, except that we use different tools to manage it and have a different focus (as we’ll discuss).

在这种程度上，SRE的自动化工作与其他许多人和组织所做的相差无几，只是我们使用不同的工具来管理它，并且有不同的重点（我们将讨论）。

Widely available tools like Puppet, Chef, cfengine, and even Perl, which all provide ways to automate particular tasks, differ mostly in terms of the level of abstraction of the components provided to help the act of automating. A full language like Perl provides POSIX-level affordances, which in theory provide an essentially unlimited scope of automation across the APIs accessible to the system, whereas Chef and Puppet provide out-of-the-box abstractions with which services or other higher-level entities can be manipulated. The trade-off here is classic: higher-level abstractions are easier to manage and reason about, but when you encounter a "leaky abstraction," you fail systemically, repeatedly, and potentially inconsistently. For example, we often assume that pushing a new binary to a cluster is atomic; the cluster will either end up with the old version, or the new version. However, real-world behavior is more complicated: that cluster’s network can fail halfway through; machines can fail; communication to the cluster management layer can fail, leaving the system in an inconsistent state; depending on the situation, new binaries could be staged but not pushed, or pushed but not restarted, or restarted but not verifiable. Very few abstractions model these kinds of outcomes successfully, and most generally end up halting themselves and calling for intervention. Truly bad automation systems don’t even do that.

像Puppet、Chef、cfengine，甚至Perl这样广泛使用的工具，都提供了自动化特定任务的方法，其主要区别在于为帮助自动化行为而提供的组件的抽象水平。像Perl这样的完整语言提供了POSIX级别的能力，在理论上为系统可访问的API提供了本质上无限的自动化范围，而Chef和Puppet则提供了开箱即用的抽象，可以操纵服务或其他更高级别的实体。这里的权衡是典型的：更高层次的抽象更容易管理和推理，但当你遇到一个“泄漏的抽象”时，你就会系统地、反复地失败，而且可能是不一致的。例如，我们经常假设向集群推送一个新的二进制文件是原子性的；集群最终要么用旧版本，要么用新版本。然而，现实世界的行为更为复杂：该集群的网络可能在中途发生故障；机器可能发生故障；与集群控制面的通信可能发生故障，使系统处于不一致的状态；根据情况，新的二进制文件可能被分期但没有被推送，或者被推送但没有重新启动，或者重新启动但无法验证。很少有抽象模型能成功地模拟这类结果，大多数的抽象模型通常最终会停止自己的工作并要求进行干预。真正糟糕的自动化系统甚至不会这样做。

SRE has a number of philosophies and products in the domain of automation, some of which look more like generic rollout tools without particularly detailed modeling of higher-level entities, and some of which look more like languages for describing service deployment (and so on) at a very abstract level. Work done in the latter tends to be more reusable and be more of a common platform than the former, but the complexity of our production environment sometimes means that the former approach is the most immediately tractable option.

SRE在自动化领域有很多理念和产品，其中一些看起来更像是通用的工具，没有特别详细的高层实体建模，而一些看起来更像是在非常抽象的层面上描述服务部署（等等）的语言。在后者中完成的工作往往比前者更容易重用，并且是一个共同的平台，但是我们的生产环境的复杂性有时意味着前者的方法是最直接可行的选择。

<br>

### **A Hierarchy of Automation Classes**

### **自动化类的层次结构**

Although all of these automation steps are valuable, and indeed an automation platform is valuable in and of itself, in an ideal world, we wouldn’t need externalized automation. In fact, instead of having a system that has to have external glue logic, it would be even better to have a system that needs no glue logic at all, not just because internalization is more efficient (although such efficiency is useful), but because it has been designed to not need glue logic in the first place. Accomplishing that involves taking the use cases for glue logic—generally "first order" manipulations of a system, such as adding accounts or performing system turnup—and finding a way to handle those use cases directly within the application.

尽管所有这些自动化步骤都是有价值的，事实上，自动化平台本身也是有价值的，在一个理想的世界里，我们不需要外部化的自动化。事实上，与其拥有一个必须有外部胶水逻辑的系统，不如拥有一个完全不需要胶水逻辑的系统，这不仅仅是因为内部化更有效率（尽管这种效率是有用的），而是因为它被设计为首先不需要胶水逻辑。要做到这一点，需要考虑胶水逻辑的用例--通常是对系统的“第一顺序”操作，如添加账户或执行系统启动，并找到一种方法来直接在应用程序中处理这些用例。

As a more detailed example, most turnup automation at Google is problematic because it ends up being maintained separately from the core system and therefore suffers from "bit rot," i.e., not changing when the underlying systems change. Despite the best of intentions, attempting to more tightly couple the two (turnup automation and the core system) often fails due to unaligned priorities, as product developers will, not unreasonably, resist a test deployment requirement for every change. Secondly, automation that is crucial but only executed at infrequent intervals and therefore difficult to test is often particularly fragile because of the extended feedback cycle. Cluster failover is one classic example of infrequently executed automation: failovers might only occur every few months, or infrequently enough that inconsistencies between instances are introduced. The evolution of automation follows a path:

1. **No automation**. Database master is failed over manually between locations.
2. **Externally maintained system-specific automation**. An SRE has a failover script in his or her home directory.
3. **Externally maintained generic automation**. The SRE adds database support to a "generic failover" script that everyone uses.
4. **Internally maintained system-specific automation**. The database ships with its own failover script.
5. **Systems that don’t need any automation**. The database notices problems, and automatically fails over without human intervention.

作为一个更详细的例子，Google的大部分turnup自动化是有问题的，因为它最终与核心系统分开维护，因此受到“比特腐烂”的影响，也就是说，当底层系统改变时，它不会改变。尽管试图更紧密地结合两者（转发自动化和核心系统）往往由于不一致的优先级而失败，因为产品开发人员将抵制每一个变化的测试部署要求。其次，由于反馈周期的延长，那些至关重要但只在不频繁的时间段内执行的自动化往往特别脆弱，因此难以测试。集群故障切换是不经常执行的自动化的一个典型例子：故障切换可能每隔几个月才发生一次，或者不经常发生，以至于引入了实例之间的不一致。自动化的演变遵循一个路径：

1. **没有自动化**。数据库主站在不同地点之间手动进行故障切换。
2. **外部维护的系统特定自动化**。一个SRE在他或她的主目录中拥有一个故障转移脚本。
3. **外部维护的通用自动化**。SRE将数据库支持添加到每个人都使用的“通用故障转移”脚本中。
4. **内部维护的系统特定自动化**。数据库有它自己的故障转移脚本。
5. **不需要任何自动化的系统**。数据库会注意到问题，并自动进行故障转移，无需人工干预。

SRE hates manual operations, so we obviously try to create systems that don’t require them. However, sometimes manual operations are unavoidable.

SRE讨厌手动运维，所以我们显然要努力创建不需要手动运维的系统。然而，有时手动运维是不可避免的。

There is additionally a subvariety of automation that applies changes not across the domain of specific system-related configuration, but across the domain of production as a whole. In a highly centralized proprietary production environment like Google’s, there are a large number of changes that have a non–service-specific scope—e.g., changing upstream Chubby servers, a flag change to the Bigtable client library to make access more reliable, and so on—which nonetheless need to be safely managed and rolled back if necessary. Beyond a certain volume of changes, it is infeasible for production-wide changes to be accomplished manually, and at some time before that point, it’s a waste to have manual oversight for a process where a large proportion of the changes are either trivial or accomplished successfully by basic relaunch-and- check strategies.

此外，还有一个自动化的子品种，它不是在特定的系统相关配置领域，而是在整个生产领域应用变化。在像Google这样高度集中的专有生产环境中，有大量的变化是不针对服务的，例如，改变上游的Chubby服务器，改变Bigtable客户端库的标志以使访问更可靠等等，这些变化仍然需要被安全地管理，并在必要时回滚。如果超过一定的变化量，在整个生产过程中手动完成变化是不可行的，而在这之前的某个时间，对一个过程进行手动监督是一种浪费。在这个过程中，大部分的变化是微不足道的，或者通过基本的重新启动和检查策略成功完成。

Let’s use internal case studies to illustrate some of the preceding points in detail. The first case study is about how, due to some diligent, far-sighted work, we managed to achieve the self-professed nirvana of SRE: to automate ourselves out of a job.

让我们用内部案例研究来详细说明前面的一些观点。第一个案例研究是关于由于一些勤奋的、有远见的工作，我们成功地实现了自称的SRE的涅槃：把自己从工作中自动化出来。

<br>

---

**[Back to contents of the chapter（返回章节目录）](the_evolution_of_automation_at_google.md)**

* **Previous Section（上一节）：[The Value for Google SRE（Google SRE的价值）](the_value_of_google_sre.md)**
* **Next Section（下一节）：[Automate Yourself Out of a Job: Automate ALL the Things!（让自己的工作自动化：把所有的事情都自动化!）](automate_yourself_out_of_a_job.md)**
