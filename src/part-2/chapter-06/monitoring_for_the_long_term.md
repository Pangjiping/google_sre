## **Monitoring for the Long Term**

## **长期监控**

In modern production systems, monitoring systems track an ever-evolving system with changing software architecture, load characteristics, and performance targets. An alert that’s currently exceptionally rare and hard to automate might become frequent, perhaps even meriting a hacked-together script to resolve it. At this point, someone should find and eliminate the root causes of the problem; if such resolution isn’t possible, the alert response deserves to be fully automated.

在现代生产系统中，监控系统跟踪一个不断发展的系统，其软件架构、负载特性和性能目标都在变化。一个目前非常罕见的、难以自动化的警报可能会变得频繁，也许甚至值得用一个黑客拼凑的脚本来解决它。在这一点上，应该有人找到并消除问题的根源；如果这种解决方法不可能，那么警报响应就应该完全自动化。

It’s important that decisions about monitoring be made with long-term goals in mind. Every page that happens today distracts a human from improving the system for tomorrow, so there is often a case for taking a short-term hit to availability or performance in order to improve the long-term outlook for the system. Let’s take a look at two case studies that illustrate this trade-off.

重要的是，关于监控的决定应考虑到长期目标。今天发生的每一个呼叫都会分散人们为明天改进系统的注意力，所以为了改善系统的长期前景而对可用性或性能进行短期舍弃往往是合理的。让我们来看看两个说明这种权衡的案例研究。

<br>

### **Bigtable SRE: A Tale of Over-Alerting**

### **Bigtable SRE: 过度警报的故事**

Google’s internal infrastructure is typically offered and measured against a service level objective (SLO; see Chapter 4). Many years ago, the Bigtable service’s SLO was based on a synthetic well-behaved client’s mean performance. Because of problems in Bigtable and lower layers of the storage stack, the mean performance was driven by a "large" tail: the worst 5% of requests were often significantly slower than the rest.

谷歌的内部基础设施通常是根据[SLO](./../chapter-04/service_level_objectives.md)来提供和衡量的。许多年前，Bigtable服务的SLO是基于一个合成的行为良好的客户端的平均性能。由于Bigtable和存储栈下层的问题，平均性能被“大”拖尾所驱动：最差的5%的请求往往比其他请求慢得多。

Email alerts were triggered as the SLO approached, and paging alerts were triggered when the SLO was exceeded. Both types of alerts were firing voluminously, consuming unacceptable amounts of engineering time: the team spent significant amounts of time triaging the alerts to find the few that were really actionable, and we often missed the problems that actually affected users, because so few of them did. Many of the pages were non-urgent, due to well-understood problems in the infrastructure, and had either rote responses or received no response.

当SLO接近时，电子邮件警报被触发，而当SLO被超过时，寻呼警报被触发。这两种类型的警报都是大量发送的，消耗了大量的工程时间：团队花了大量的时间对警报进行分流，以找到少数真正可操作的警报，我们经常错过真正影响用户的问题，因为这些问题太少。许多呼叫是不紧急的，因为基础设施中存在众所周知的问题，而且要么是照本宣科的回应，要么是没有得到回应。

To remedy the situation, the team used a three-pronged approach: while making great efforts to improve the performance of Bigtable, we also temporarily dialed back our SLO target, using the 75th percentile request latency. We also disabled email alerts, as there were so many that spending time diagnosing them was infeasible.

为了修复这种情况，团队采用了三管齐下的方法：在努力提高Bigtable的性能的同时，我们也暂时调低了我们的SLO目标，使用75%的请求延迟。我们还禁用了电子邮件警报，因为警报太多，花时间去诊断它们是不可行的。

This strategy gave us enough breathing room to actually fix the longer-term problems in Bigtable and the lower layers of the storage stack, rather than constantly fixing tactical problems. On-call engineers could actually accomplish work when they weren’t being kept up by pages at all hours. Ultimately, temporarily backing off on our alerts allowed us to make faster progress toward a better service.

这种策略给了我们足够的喘息空间，使我们能够真正解决Bigtable和存储堆栈底层的长期问题，而不是不断修复问题。当值班的工程师们不需要在任何时候都被呼叫催促时，他们可以真正完成工作。最终，暂时减少警报使我们能够更快地实现更好的服务。

<br>

### **Gmail: Predictable, Scriptable Responses from Humans**

### **Gmail：来自人类的可预测的、可编写脚本的回应**

In the very early days of Gmail, the service was built on a retrofitted distributed process management system called Workqueue, which was originally created for batch processing of pieces of the search index. Workqueue was "adapted" to long-lived processes and subsequently applied to Gmail, but certain bugs in the relatively opaque codebase in the scheduler proved hard to beat.

在Gmail的早期，该服务是建立在一个名为Workqueue的改装的分布式进程管理系统上的，该系统最初是为批量处理搜索索引的碎片而创建的。Workqueue被“改编”为长寿命进程，并随后应用于Gmail，但事实证明，调度器中相对不透明的代码库中的某些错误很难被察觉。

At that time, the Gmail monitoring was structured such that alerts fired when individual tasks were "de-scheduled" by Workqueue. This setup was less than ideal because even at that time, Gmail had many, many thousands of tasks, each task representing a fraction of a percent of our users. We cared deeply about providing a good user experience for Gmail users, but such an alerting setup was unmaintainable.

当时，Gmail监控的结构是，当个别任务被Workqueue“取消计划”时，就发出警报。这种设置并不理想，因为即使在那个时候，Gmail也有很多很多的任务，每个任务只占我们用户的百分之几。我们非常关心为Gmail用户提供良好的用户体验，但这样的警报设置是无法维持的。

To address this problem, Gmail SRE built a tool that helped "poke" the scheduler in just the right way to minimize impact to users. The team had several discussions about whether or not we should simply automate the entire loop from detecting the problem to nudging the rescheduler, until a better long-term solution was achieved, but some worried this kind of workaround would delay a real fix.

为了解决这个问题，Gmail SRE建立了一个工具，帮助以正确的方式“捅”一下调度器，以尽量减少对用户的影响。团队曾多次讨论过，我们是否应该简单地把从检测问题到催促重新调度器的整个循环自动化，直到实现一个更好的长期解决方案，但有人担心这种变通方法会拖延真正的修复。

This kind of tension is common within a team, and often reflects an underlying mistrust of the team’s self-discipline: while some team members want to implement a "hack" to allow time for a proper fix, others worry that a hack will be forgotten or that the proper fix will be deprioritized indefinitely. This concern is credible, as it’s easy to build layers of unmaintainable technical debt by patching over problems instead of making real fixes. Managers and technical leaders play a key role in implementing true, long-term fixes by supporting and prioritizing potentially time- consuming long-term fixes even when the initial "pain" of paging subsides.

这种紧张关系在团队中很常见，而且往往反映了对团队自律的潜在不信任：一些团队成员希望实施“黑客”，以便有时间进行适当的修复，而其他人则担心黑客会被遗忘，或者适当的修复会被无限期地取消优先级。这种担心是可信的，因为在问题上打补丁而不是进行真正的修复，很容易建立起一层层不可维护的技术债务。管理人员和技术领导在实施真正的、长期的修复方面发挥着关键作用，他们支持并优先考虑可能耗费时间的长期修复，即使在最初的呼叫“痛苦”消退之后。

Pages with rote, algorithmic responses should be a red flag. Unwillingness on the part of your team to automate such pages implies that the team lacks confidence that they can clean up their technical debt. This is a major problem worth escalating.

带有死记硬背的算法反应的呼叫应该是一个红旗。你的团队不愿意将这些呼叫自动化，意味着该团队缺乏信心，认为他们可以清理他们的技术债务。这是一个值得升级的重大问题。

<br>

### **The Long Run**

### **长期运行**

A common theme connects the previous examples of Bigtable and Gmail: a tension between short-term and long-term availability. Often, sheer force of effort can help a rickety system achieve high availability, but this path is usually short-lived and fraught with burnout and dependence on a small number of heroic team members. Taking a controlled, short-term decrease in availability is often a painful, but strategic trade for the long-run stability of the system. It’s important not to think of every page as an event in isolation, but to consider whether the overall level of paging leads toward a healthy, appropriately available system with a healthy, viable team and long-term outlook. We review statistics about page frequency (usually expressed as incidents per shift, where an incident might be composed of a few related pages) in quarterly reports with management, ensuring that decision makers are kept up to date on the pager load and overall health of their teams.

一个共同的主题连接着前面的Bigtable和Gmail的例子：短期和长期可用性之间的矛盾。通常，纯粹的努力可以帮助一个摇摇欲坠的系统实现高可用性，但这条道路通常是短暂的，充满了倦怠和对少数团队成员的依赖。采取可控的、短期的降低可用性的做法往往是一种痛苦的、但对系统的长期稳定性来说是战略性的无权衡。重要的是，不要把每一个呼叫看作是一个孤立的事件，而是要考虑整体的寻呼水平是否导致一个健康的、适当的可用系统，以及一个健康的、可行的团队和长期前景。我们在与管理层的季度报告中审查有关传呼频率的统计数据（通常表示为每班的事件，其中一个事件可能由几个相关的传呼组成），确保决策者能够及时了解传呼机的负载和团队的整体健康状况。
