## **Reliability Is the Fundamental Feature**

## **可靠性是最基本的特征**

Of course, for effective troubleshooting, the details of internal operation that the introspection relies upon should also be exposed to the humans managing the overall system. Analogous discussions about the impact of automation in the noncomputer domain—for example, in airplane flight or industrial applications—often point out the downside of highly effective automation: human operators are progressively more relieved of useful direct contact with the system as the automation covers more and more daily activities over time. Inevitably, then, a situation arises in which the automation fails, and the humans are now unable to successfully operate the system.

当然，为了有效地排除故障，所依赖的内部操作细节也应该暴露给管理整个系统的人们。关于自动化在非计算机领域的影响的类似讨论--例如，在飞机飞行或工业应用中--常常指出高度有效的自动化的缺点：随着时间的推移，自动化覆盖了越来越多的日常活动，人类操作员逐渐失去了与系统直接接触的机会。因此，不可避免地会出现自动化失败的情况，而人类现在无法成功地操作系统。

The fluidity of their reactions has been lost due to lack of practice, and their mental models of what the system should be doing no longer reflect the reality of what it is doing.10 This situation arises more when the system is nonautonomous—i.e., where automation replaces manual actions, and the manual actions are presumed to be always performable and available just as they were before. Sadly, over time, this ultimately becomes false: those manual actions are not always performable because the functionality to permit them no longer exists.

由于缺乏实践，他们的反应的流畅性已经丧失，他们对系统应该做什么的心智模式不再反映系统正在做什么的现实。可悲的是，随着时间的推移，这最终变成了错误：那些手工操作并不总是可以执行的，因为允许它们的功能已经不存在了。

We, too, have experienced situations where automation has been actively harmful on a number of occasions—see "Automation: Enabling Failure at Scale" on page 85—but in Google’s experience, there are more systems for which automation or autonomous behavior are no longer optional extras. As you scale, this is of course the case, but there are still strong arguments for more autonomous behavior of systems irrespective of size. Reliability is the fundamental feature, and autonomous, resilient behavior is one useful way to get that.

我们也曾经历过自动化在一些情况下是有害的--见“自动化：启用规模化的故障”但根据Google的经验，有更多的系统的自动化或自主行为不再是可有可无的东西了。随着规模的扩大，情况当然也是如此，但无论规模大小，对系统的更多自主行为仍有强有力的论据。可靠性是最基本的特征，而自主的、有弹性的行为是获得这一特征的一个有效途径。

> **Automation: Enabling Failure at Scale**
>
> **自动化：启用规模化的故障**
>
> Google runs over a dozen of its own large datacenters, but we also depend on machines in many third-party colocation facilities (or "colos"). Our machines in these colos are used to terminate most incoming connections, or as a cache for our own Content Delivery Network, in order to lower end-user latency. At any point in time, a number of these racks are being installed or decommissioned; both of these processes are largely automated. One step during decommission involves overwriting the full content of the disk of all the machines in the rack, after which point an independent system verifies the successful erase. We call this process "Diskerase."
>
> Google有十几个自己的大型数据中心，但我们也依赖许多第三方主机托管设施（或“colos”）中的机器。我们在这些机房中的机器被用来终止大多数传入的连接，或作为我们自己的内容交付网络的缓存，以降低终端用户的延迟。在任何时候，这些机架中的一些正在安装或下线；这两个过程在很大程度上是自动化的。在下线过程中，有一个步骤涉及到覆盖机架上所有机器的磁盘的全部内容，在这之后，一个独立的系统会验证擦除是否成功。我们把这个过程称为 “Diskerase”。
>
> Once upon a time, the automation in charge of decommissioning a particular rack failed, but only after the Diskerase step had completed successfully. Later, the decommission process was restarted from the beginning, to debug the failure. On that iteration, when trying to send the set of machines in the rack to Diskerase, the automation determined that the set of machines that still needed to be Diskerased was (correctly) empty. Unfortunately, the empty set was used as a special value, interpreted to mean "everything." This means the automation sent almost all the machines we have in all colos to Diskerase.
>
> 很久以前，负责下线某个机架的自动化系统失败了，但只是在Diskerase步骤成功完成之后。后来，下线过程被从头开始重新启动，以调试故障。在那个迭代过程中，当试图将机架中的机器集发送到Diskerase时，自动化确定仍然需要被Diskerase的机器集是（正确地）空的。不幸的是，空集被作为一个特殊的值，被解释为意味着“一切”。这意味着自动化系统将我们所有colos中的几乎所有机器都送到了Diskerase。
>
> Within minutes, the highly efficient Diskerase wiped the disks on all machines in our CDN, and the machines were no longer able to terminate connections from users (or do anything else useful). We were still able to serve all the users from our own datacenters, and after a few minutes the only effect visible externally was a slight increase in latency. As far as we could tell, very few users noticed the problem at all, thanks to good capacity planning (at least we got that right!). Meanwhile, we spent the better part of two days reinstalling the machines in the affected colo racks; then we spent the following weeks auditing and adding more sanity checks—including rate limiting— into our automation, and making our decommission workflow idempotent.
>
> 在几分钟内，高效的Diskerase擦除了我们CDN中所有机器上的磁盘，这些机器不再能够终止用户的连接（或做任何其他有用的事情）。我们仍然能够从我们自己的数据中心为所有的用户提供服务，几分钟后，外部可见的唯一影响是延迟的轻微增加。据我们所知，由于良好的容量规划（至少我们做对了！），很少有用户注意到这个问题。同时，我们花了两天的时间在受影响的主机架上重新安装机器；然后我们花了几周的时间在自动化中审核和增加更多的理智检查（包括速率限制），并使我们的下线工作流变得无所作为。

<br>

---

**[Back to contents of the chapter（返回章节目录）](the_evolution_of_automation_at_google.md)**

* **Previous Section（上一节）：[Borg: Birth of the Warehouse-Scale Computer（Borg：仓库级计算机的诞生）](borg.md)**
* **Next Section（下一节）：[Recommendations（建议）](recommendations.md)**
