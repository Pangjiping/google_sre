# **Principles**

# **原则**

This section examines the principles underlying how SRE teams typically work—the patterns, behaviors, and areas of concern that influence the general domain of SRE operations.

本部分研究了SRE团队通常如何工作的基本原则--影响SRE运作的一般领域的模式、行为和关注领域。

The first chapter in this section, and the most important piece to read if you want to attain the widest-angle picture of what exactly SRE does, and how we reason about it, is [Chapter 3, Embracing Risk](./chapter-03/embracing_risk.md). It looks at SRE through the lens of risk—its assessment, management, and the use of error budgets to provide usefully neutral approaches to service management.

本节的第一章，也是最重要的一章，如果你想从最广泛的角度了解SRE到底是做什么的，以及我们是如何进行推理的，那就是[第三章，拥抱风险](./chapter-03/embracing_risk.md)。它通过风险的视角来看待SRE--它的评估、管理和使用错误预算来为服务管理提供有益的中立方法。

Service level objectives are another foundational conceptual unit for SRE. The industry commonly lumps disparate concepts under the general banner of service level agreements, a tendency that makes it harder to think about these concepts clearly. [Chapter 4, Service Level Objectives](./chapter-04/service_level_objectives.md), attempts to disentangle indicators from objectives from agreements, examines how SRE uses each of these terms, and provides some recommendations on how to find useful metrics for your own applications.

服务水平目标是SRE的另一个基础概念单元。业界通常把不同的概念放在服务水平协议的总旗帜下，这种倾向使人们更难清楚地思考这些概念。[第4章，服务水平目标](./chapter-04/service_level_objectives.md)，试图把指标和目标从协议中分离出来，研究SRE如何使用这些术语，并提供一些关于如何为你自己的应用找到有用的指标的建议。

Eliminating toil is one of SRE’s most important tasks, and is the subject of [Chapter 5, Eliminating Toil](./chapter-05/eliminating_toil.md). We define toil as mundane, repetitive operational work providing no enduring value, which scales linearly with service growth.

消除劳作是SRE最重要的任务之一，也是[第5章，消除劳作](./chapter-05/eliminating_toil.md)的主题。我们将劳作定义为平凡的、重复性的运维性工作，不提供持久的价值，它随着服务的增长而线性扩展。

Whether it is at Google or elsewhere, monitoring is an absolutely essential component of doing the right thing in production. If you can’t monitor a service, you don’t know what’s happening, and if you’re blind to what’s happening, you can’t be reliable. Read [Chapter 6, Monitoring Distributed Systems](./chapter-06/monitoring_distributed_systems.md), for some recommendations for what and how to monitor, and some implementation-agnostic best practices.

无论是在谷歌还是其他地方，监控都是在生产中做正确事情的绝对必要组成部分。如果你不能监控服务，你就不知道发生了什么，如果你对正在发生的事情视而不见，你就不可能可靠。阅读[第6章，监控分布式系统](./chapter-06/monitoring_distributed_systems.md)，了解关于监控什么和如何监控的一些建议，以及一些与实现无关的最佳实践。

In [Chapter 7, The Evolution of Automation at Google](./chapter-07/the_evolution_of_automation_at_google.md), we examine SRE’s approach to automation, and walk through some case studies of how SRE has implemented automation, both successfully and unsuccessfully.

在[第7章，谷歌自动化的进程](./chapter-07/the_evolution_of_automation_at_google.md)，我们研究了SRE的自动化方法，并通过一些案例研究SRE如何实现自动化，无论是成功的还是失败的。

Most companies treat release engineering as an afterthought. However, as you’ll learn in [Chapter 8, Release Engineering](./chapter-08/release_engineering.md), release engineering is not just critical to overall system stability—as most outages result from pushing a change of some kind. It is also the best way to ensure that releases are consistent.

大多数公司将发布工程视为事后的想法。然而，正如您将在[第8章，发布工程](./chapter-08/release_engineering.md)中了解到的那样，发布工程不仅对整体系统稳定性至关重要——因为大多数中断都是由发布某种更改引起的。这也是确保发布一致的最佳方式。

A key principle of any effective software engineering, not only reliability-oriented engineering, simplicity is a quality that, once lost, can be extraordinarily difficult to recapture. Nevertheless, as the old adage goes, a complex system that works necessarily evolved from a simple system that works. [Chapter 9, Simplicity](./chapter-09/simplicity.md), goes into this topic in detail.

任何有效软件工程的关键原则，不仅仅是面向可靠性的工程，简单性是一种一旦失去就很难重新获得的品质。然而，正如一句古老的格言所说，一个有效的复杂系统必然是从一个有效的简单系统演变而来的。[第9章，简单性](./chapter-09/simplicity.md)，详细讨论了这个主题。
