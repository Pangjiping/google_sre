# **Principles**

# **原则**

This section examines the principles underlying how SRE teams typically work—the patterns, behaviors, and areas of concern that influence the general domain of SRE operations.

本部分研究了SRE团队通常如何工作的基本原则--影响SRE运作的一般领域的模式、行为和关注领域。

The first chapter in this section, and the most important piece to read if you want to attain the widest-angle picture of what exactly SRE does, and how we reason about it, is [Chapter 3](./chapter-03/embracing_risk.md), Embracing Risk. It looks at SRE through the lens of risk—its assessment, management, and the use of error budgets to provide usefully neutral approaches to service management.

本节的第一章，也是最重要的一章，如果你想从最广泛的角度了解SRE到底是做什么的，以及我们是如何进行推理的，那就是[第三章](./chapter-03/embracing_risk.md)，拥抱风险。它通过风险的视角来看待SRE--它的评估、管理和使用错误预算来为服务管理提供有益的中立方法。

Service level objectives are another foundational conceptual unit for SRE. The industry commonly lumps disparate concepts under the general banner of service level agreements, a tendency that makes it harder to think about these concepts clearly. [Chapter 4](./chapter-04/service_level_objectives.md), Service Level Objectives, attempts to disentangle indicators from objectives from agreements, examines how SRE uses each of these terms, and provides some recommendations on how to find useful metrics for your own applications.

服务水平目标是SRE的另一个基础概念单元。业界通常把不同的概念放在服务水平协议的总旗帜下，这种倾向使人们更难清楚地思考这些概念。[第4章](./chapter-04/service_level_objectives.md)，服务水平目标，试图把指标和目标从协议中分离出来，研究SRE如何使用这些术语，并提供一些关于如何为你自己的应用找到有用的指标的建议。

Eliminating toil is one of SRE’s most important tasks, and is the subject of Chapter 5, Eliminating Toil. We define toil as mundane, repetitive operational work providing no enduring value, which scales linearly with service growth.

Whether it is at Google or elsewhere, monitoring is an absolutely essential component of doing the right thing in production. If you can’t monitor a service, you don’t know what’s happening, and if you’re blind to what’s happening, you can’t be reliable. Read Chapter 6, Monitoring Distributed Systems, for some recommendations for what and how to monitor, and some implementation-agnostic best practices.

In Chapter 7, The Evolution of Automation at Google, we examine SRE’s approach to automation, and walk through some case studies of how SRE has implemented automation, both successfully and unsuccessfully.

Most companies treat release engineering as an afterthought. However, as you’ll learn in Chapter 8, Release Engineering, release engineering is not just critical to overall system stability—as most outages result from pushing a change of some kind. It is also the best way to ensure that releases are consistent.

A key principle of any effective software engineering, not only reliability-oriented engineering, simplicity is a quality that, once lost, can be extraordinarily difficult to recapture. Nevertheless, as the old adage goes, a complex system that works necessarily evolved from a simple system that works. Chapter 9, Simplicity, goes into this topic in detail.
