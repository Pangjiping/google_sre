## **Google’s Approach to Service Management:Site Reliability Engineering**

## **谷歌的服务管理方法：SRE**

Conflict isn’t an inevitable part of offering a software service. Google has chosen to run our systems with a different approach: our Site Reliability Engineering teams focus on hiring software engineers to run our products and to create systems to accomplish the work that would otherwise be performed, often manually, by sysadmins.

冲突不是提供软件服务的必然部分。谷歌选择以不同的方式运行我们的系统：我们的SRE团队专注于聘用软件工程师来运行我们的产品，并创建系统来完成通常需要系统管理员手动完成的工作。

What exactly is Site Reliability Engineering, as it has come to be defined at Google? My explanation is simple: SRE is what happens when you ask a software engineer to design an operations team. When I joined Google in 2003 and was tasked with running a “Production Team” of seven engineers, my entire life up to that point had been software engineering. So I designed and managed the group the way I would want it to work if I worked as an SRE myself. That group has since matured to become Google’s present-day SRE team, which remains true to its origins as envisioned by a lifelong software engineer.

谷歌所定义的站点可靠性工程（Site Reliability Engineering，简称SRE）到底是什么？我的解释很简单：SRE就是当你让一个软件工程师来设计一个运维团队时会发生什么。当我在2003年加入谷歌，负责管理一个由七名工程师组成的“生产团队”时，我之前的全部经历都是软件工程。因此，我设计和管理这个团队的方式就是我自己如果当一个SRE，我想它能够工作的方式。这个团队后来发展成为了谷歌现在的SRE团队，始终忠于一个终身软件工程师构想的初衷。

A primary building block of Google’s approach to service management is the composition of each SRE team. As a whole, SRE can be broken down two main categories.

谷歌服务管理方法的主要构建块是每个SRE团队的组成。整个SRE团队可以分为两大类别。

50–60% are Google Software Engineers, or more precisely, people who have been hired via the standard procedure for Google Software Engineers. The other 40–50% are candidates who were very close to the Google Software Engineering qualifications (i.e., 85–99% of the skill set required), and who in addition had a set of technical skills that is useful to SRE but is rare for most software engineers. By far, UNIX system internals and networking (Layer 1 to Layer 3) expertise are the two most common types of alternate technical skills we seek.

50%到60%的SRE团队成员是谷歌软件工程师，或者更准确地说，是通过谷歌软件工程师的标准程序招聘而来的人员。另外40%到50%的成员则是那些非常接近谷歌软件工程师资格要求的候选人（即技能要求的85%到99%之间），并且具备对SRE有用但对大多数软件工程师而言较为罕见的技术技能。在这些技能中，UNIX系统内部和网络（从第一层到第三层）专业知识是我们寻求的两种最常见的备选技能类型。

Common to all SREs is the belief in and aptitude for developing software systems to solve complex problems. Within SRE, we track the career progress of both groups closely, and have to date found no practical difference in performance between engineers from the two tracks. In fact, the somewhat diverse background of the SRE team frequently results in clever, high-quality systems that are clearly the product of the synthesis of several skill sets.

所有SRE团队成员都有一个共同点，那就是他们相信并具备开发软件系统来解决复杂问题的能力。在SRE内部，我们密切关注两组工程师的职业发展进程，并且迄今为止，我们发现两个轨道的工程师之间的表现没有实际差异。事实上，SRE团队的略微多样化的背景经常会生产出巧妙而高质量的系统，这些系统显然是几种技能综合的产物。

The result of our approach to hiring for SRE is that we end up with a team of people who (a) will quickly become bored by performing tasks by hand, and (b) have the skill set necessary to write software to replace their previously manual work, even when the solution is complicated. SREs also end up sharing academic and intellectual background with the rest of the development organization. Therefore, SRE is fundamentally doing work that has historically been done by an operations team, but using engineers with software expertise, and banking on the fact that these engineers are inherently both predisposed to, and have the ability to, design and implement automation with software to replace human labor.

我们招聘SRE的方法的结果是，我们最终得到了一支团队，他们很快就会厌倦手动执行任务，以及具备编写软件以替代以前的手动工作所需的技能，即使解决方案很复杂。SRE团队的学术和智力背景也与开发组织的其他部分相似。因此，SRE团队本质上是在做一个以前由运维团队完成的工作，但是使用具备软件专业知识的工程师，而且我们相信这些工程师天生具备设计和实施自动化软件以取代人力的倾向和能力。

By design, it is crucial that SRE teams are focused on engineering. Without constant engineering, operations load increases and teams will need more people just to keep pace with the workload. Eventually, a traditional ops-focused group scales linearly with service size: if the products supported by the service succeed, the operational load will grow with traffic. That means hiring more people to do the same tasks over and over again.

SRE团队专注于工程。没有不断的工程支持，运维负担会增加，团队需要更多的人来跟上工作量。最终，一个传统的运维团队的规模会随着服务规模线性增长：如果服务支持的产品取得成功，操作负载将随着流量增长而增加。这意味着需要雇用更多的人来反复执行相同的任务。

To avoid this fate, the team tasked with managing a service needs to code or it will drown. Therefore, Google places a 50% cap on the aggregate “ops” work for all SREs— tickets, on-call, manual tasks, etc. This cap ensures that the SRE team has enough time in their schedule to make the service stable and operable. This cap is an upper bound; over time, left to their own devices, the SRE team should end up with very little operational load and almost entirely engage in development tasks, because the service basically runs and repairs itself: we want systems that are automatic, not just automated. In practice, scale and new features keep SREs on their toes.

为了避免这种命运，负责管理服务的团队需要进行编码，否则他们将被大量任务拖垮。因此，Google为所有SRE团队制定了一个“运维”工作的总量上限，包括票务、值班、手动任务等，占总工作量的50%。这个上限确保SRE团队有足够的时间来使服务稳定和可操作。这个上限是一个上限，随着时间的推移，SRE团队应该有很少的运营负载，几乎完全从事开发任务，因为服务基本上运行和修复自己：我们需要的是自动的系统，而不仅仅是自动化的系统。实际上，规模和新功能使SRE团队保持警惕。

Google’s rule of thumb is that an SRE team must spend the remaining 50% of its time actually doing development. So how do we enforce that threshold? In the first place, we have to measure how SRE time is spent. With that measurement in hand, we ensure that the teams consistently spending less than 50% of their time on development work change their practices. Often this means shifting some of the operations burden back to the development team, or adding staff to the team without assigning that team additional operational responsibilities. Consciously maintaining this balance between ops and development work allows us to ensure that SREs have the bandwidth to engage in creative, autonomous engineering, while still retaining the wisdom gleaned from the operations side of running a service.

谷歌的经验法则是，SRE团队必须将其50%的时间用于实际开发。那么，我们如何执行这个阈值呢？首先，我们必须测算SRE时间的分配情况。有了这个数据，我们确保团队始终将少于50%的时间用于开发工作，并改变他们的工作实践。通常，这意味着将一些运维负担转移回开发团队，或者增加团队成员，而不给团队分配额外的运维责任。有意识地维护这种运维和开发工作的平衡，可以确保SRE有足够的时间进行创造性的、自治的工程开发，同时仍然保留从运维角度运行服务所获得的经验。

We’ve found that Google SRE’s approach to running large-scale systems has many advantages. Because SREs are directly modifying code in their pursuit of making Google’s systems run themselves, SRE teams are characterized by both rapid innovation and a large acceptance of change. Such teams are relatively inexpensive—supporting the same service with an ops-oriented team would require a significantly larger number of people. Instead, the number of SREs needed to run, maintain, and improve a system scales sublinearly with the size of the system. Finally, not only does SRE circumvent the dysfunctionality of the dev/ops split, but this structure also improves our product development teams: easy transfers between product development and SRE teams cross-train the entire group, and improve skills of developers who otherwise may have difficulty learning how to build a million-core distributed system.

我们发现谷歌SRE运维大规模系统的方法有许多优势。因为SRE直接修改代码以使谷歌的系统自动运行，所以SRE团队具有快速创新和对大量变更的接受程度。这样的团队相对低成本——用运维为导向的团队来支持同一服务需要更多的人员。相反，运行、维护和改进系统所需的SRE数量与系统的规模成非线性比例关系。最后，SRE不仅避免了开发和运维之间的不协调，而且这种结构还改善了我们的产品开发团队：产品开发和SRE团队之间的易于转移使整个团队进行了交叉培训，提高了开发人员的技能，否则他们可能难以学习如何构建一个百万核心的分布式系统。

Despite these net gains, the SRE model is characterized by its own distinct set of challenges. One continual challenge Google faces is hiring SREs: not only does SRE compete for the same candidates as the product development hiring pipeline, but the fact that we set the hiring bar so high in terms of both coding and system engineering skills means that our hiring pool is necessarily small. As our discipline is relatively new and unique, not much industry information exists on how to build and manage an SRE team (although hopefully this book will make strides in that direction!). And once an SRE team is in place, their potentially unorthodox approaches to service management require strong management support. For example, the decision to stop releases for the remainder of the quarter once an error budget is depleted might not be embraced by a product development team unless mandated by their management.

尽管存在这些净收益，SRE模式也面临着自己的一系列挑战。谷歌持续面临的一个挑战是聘请SRE：SRE不仅与产品开发招聘竞争同一候选人，而且我们在编码和系统工程技能方面设定了非常高的招聘标准，这意味着我们的招聘池必然很小。由于我们的学科相对较新且独特，行业中并没有太多有关如何构建和管理SRE团队的信息（尽管希望本书能在这方面取得进展！）。一旦建立了SRE团队，他们对服务管理的潜在非常规方法需要得到强有力的管理支持。例如，一旦错误预算用完，决定在季度剩余时间内停止发布可能不会得到产品开发团队的支持，除非被他们的管理层指示这样做。

<br>
---

**[Back to contents of the chapter（返回章节目录）](introduction.md)**

- **Previous Section（上一节）:[The Sysadmin Approach to Service Management（系统管理员的服务管理方法）](the_sysadmin_approach_to_service_management.md)**
- **Next Section（下一节）：[Tenets of SRE（SRE的原则）](tenets_of_sre.md)**
