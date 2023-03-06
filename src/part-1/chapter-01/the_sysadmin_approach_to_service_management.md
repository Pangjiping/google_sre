## **The Sysadmin Approach to Service Management**

## **系统管理员的服务管理方法**

Historically, companies have employed systems administrators to run complex computing systems.

从历史上看，公司雇佣系统管理员来运行复杂的计算系统。

This systems administrator, or sysadmin, approach involves assembling existing software components and deploying them to work together to produce a service. Sysadmins are then tasked with running the service and responding to events and updates as they occur. As the system grows in complexity and traffic volume, generating a corresponding increase in events and updates, the sysadmin team grows to absorb the additional work. Because the sysadmin role requires a markedly different skill set than that required of a product’s developers, developers and sysadmins are divided into discrete teams: “development” and “operations” or “ops.”

这种系统管理员或系统管理员方法涉及组装现有的软件组件并部署它们以协同工作，进而产生服务。然后，系统管理员的任务是运行该服务并在事件和更新发生时做出响应。随着系统复杂性和流量的增加，事件和更新也相应增加，系统管理员团队不断壮大以承担额外的工作。由于系统管理员角色需要的技能集与产品开发人员所需的技能集明显不同，因此开发人员和系统管理员被分为不同的团队：“开发”和“运维”或“ops”。

The sysadmin model of service management has several advantages. For companies deciding how to run and staff a service, this approach is relatively easy to implement: as a familiar industry paradigm, there are many examples from which to learn and emulate. A relevant talent pool is already widely available. An array of existing tools, software components (off the shelf or otherwise), and integration companies are available to help run those assembled systems, so a novice sysadmin team doesn’t have to reinvent the wheel and design a system from scratch.

服务管理的系统管理员模式有几个优点。对于决定如何运营和配备服务的公司而言，这种方法实施起来相对容易：作为一种熟悉的行业范例，有许多示例可供学习和效仿。相关人才库已经广泛可用。一系列现有工具、软件组件（现成或其他）和集成工具可用于帮助运行这些组装的系统，因此新手系统管理员团队不必重新发明轮子并从头开始设计系统。

The sysadmin approach and the accompanying development/ops split has a number of disadvantages and pitfalls. These fall broadly into two categories: direct costs and indirect costs.

系统管理员方法和伴随的开发/运维分离有许多缺点和陷阱。这些大致分为两类：直接成本和间接成本。

Direct costs are neither subtle nor ambiguous. Running a service with a team that relies on manual intervention for both change management and event handling becomes expensive as the service and/or traffic to the service grows, because the size of the team necessarily scales with the load generated by the system.

直接成本既不微妙也不模糊。随着服务和服务流量的增长，与依赖手动干预变更管理和事件处理的团队一起运行服务变得昂贵，因为团队的规模必然随着系统产生的负载而扩展。

The indirect costs of the development/ops split can be subtle, but are often more expensive to the organization than the direct costs. These costs arise from the fact that the two teams are quite different in background, skill set, and incentives. They use different vocabulary to describe situations; they carry different assumptions about both risk and possibilities for technical solutions; they have different assumptions about the target level of product stability. The split between the groups can easily become one of not just incentives, but also communication, goals, and eventually, trust and respect. This outcome is a pathology.

开发/运维拆分的间接成本可能很微妙，但对组织而言通常比直接成本更昂贵。这些成本源于两个团队在背景、技能组合和激励方面截然不同的事实。他们使用不同的词汇来描述情况；他们对技术解决方案的风险和可能性有不同的假设；他们对产品稳定性的目标水平有不同的假设。群体之间的分裂很容易成为一种激励，也是一种沟通、目标，并最终成为信任和尊重。这种结果是一种病态。

Traditional operations teams and their counterparts in product development thus often end up in conflict, most visibly over how quickly software can be released to production. At their core, the development teams want to launch new features and see them adopted by users. At their core, the ops teams want to make sure the service doesn’t break while they are holding the pager. Because most outages are caused by some kind of change—a new configuration, a new feature launch, or a new type of user traffic—the two teams’ goals are fundamentally in tension.

因此，传统的运维团队和他们在产品开发中的同事往往最终会发生冲突，最明显的是软件可以多快地投入生产。开发团队的核心是希望推出新功能并看到它们被用户采用。运维团队的核心是要确保在他们拿着寻呼机时服务不会中断。因为大多数中断是由某种变化引起的——新配置、新功能发布或新类型的用户流量——两个团队的目标从根本上是矛盾的。

Both groups understand that it is unacceptable to state their interests in the baldest possible terms (“We want to launch anything, any time, without hindrance” versus “We won’t want to ever change anything in the system once it works”). And because their vocabulary and risk assumptions differ, both groups often resort to a familiar form of trench warfare to advance their interests. The ops team attempts to safeguard the running system against the risk of change by introducing launch and change gates. For example, launch reviews may contain an explicit check for every problem that has ever caused an outage in the past—that could be an arbitrarily long list, with not all elements providing equal value. The dev team quickly learns how to respond. They have fewer “launches” and more “flag flips,” “incremental updates,” or “cherry-picks.” They adopt tactics such as sharding the product so that fewer features are subject to the launch review.

两个群体都明白，用最直白的术语来陈述他们的利益是不可接受的（“我们想在任何时候不受阻碍地推出任何东西”与“我们不想在系统运行后改变任何东西”）。而且由于他们的词汇和风险假设不同，这两个群体经常诉诸一种熟悉的壕沟战形式来促进他们的利益。运维团队试图通过引入启动和变更门槛来保护正在运行的系统免受变更风险。例如，启动审查可能包含对过去曾导致中断的每个问题的明确检查——这可能是一个任意长的列表，并非所有元素都提供相同的价值。开发团队很快就学会了如何应对。他们有更少的“启动”和更多的“标记翻转”、“增量更新”或“精选”。他们采用诸如对产品进行分片等策略，以便更少的功能需要进行发布审查。

> Flag flips（标记翻转）是一种常见的软件开发问题，通常出现在多线程或多进程的并发编程中。在这种情况下，多个线程或进程共享同一份数据，当某个线程或进程更改了某个标志位时，其他线程或进程也会受到影响。
>
> 在软件开发中，incremental updates（增量更新）指的是将一个系统、应用程序或数据集的更新内容分成多个较小的部分进行逐步更新的过程。相比于全量更新，增量更新具有更高的效率和更低的风险。
>
> cherry-pick（精选）指的是从一个代码库中选择某个特定的提交（commit），并将其应用到另一个代码库中的过程。通常情况下，cherry-pick用于在不同的代码库之间复用代码或修复特定的问题。

<br>

---

**[Back to contents of the chapter（返回章节目录）](introduction.md)**

- **Next Section（下一节）：[Google’s Approach to Service Management:Site Reliability Engineering（谷歌的服务管理方法：SRE）](google's_approach_to_service_management_site_reliability_engineering.md)**