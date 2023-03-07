## **Google’s Approach to Service Management:Site Reliability Engineering**

## **谷歌的服务管理方法：SRE**

Conflict isn’t an inevitable part of offering a software service. Google has chosen to run our systems with a different approach: our Site Reliability Engineering teams focus on hiring software engineers to run our products and to create systems to accomplish the work that would otherwise be performed, often manually, by sysadmins.

冲突不是提供软件服务的必然部分。Google选择以不同的方式运行我们的系统，我们的SRE团队聚焦于雇佣软件工程师来运行我们的产品，并创建系统来完成通常由系统管理员手动完成的工作。

What exactly is Site Reliability Engineering, as it has come to be defined at Google? My explanation is simple: SRE is what happens when you ask a software engineer to design an operations team. When I joined Google in 2003 and was tasked with running a “Production Team” of seven engineers, my entire life up to that point had been software engineering. So I designed and managed the group the way I would want it to work if I worked as an SRE myself. That group has since matured to become Google’s present-day SRE team, which remains true to its origins as envisioned by a lifelong software engineer.

Google的SRE到底是什么呢？我的解释很简单：当你让一位软件工程师来设计一个运维团队时，就会产生SRE。2003年加入Google时，我的工作是领导由七名工程师组成的“生产团队”，而我过去的整个职业生涯都是从事软件工程。因此，我设计和管理了这个团队，就像我自己成为SRE时希望它能够工作一样。这个团队现在已经发展成为Google现今的SRE团队，仍然忠实于一位终身软件工程师的愿景。

A primary building block of Google’s approach to service management is the composition of each SRE team. As a whole, SRE can be broken down two main categories.

Google的服务管理方法是每个SRE团队的构成。总体而言，SRE可以分为两大类别。

50–60% are Google Software Engineers, or more precisely, people who have been hired via the standard procedure for Google Software Engineers. The other 40–50% are candidates who were very close to the Google Software Engineering qualifications (i.e., 85–99% of the skill set required), and who in addition had a set of technical skills that is useful to SRE but is rare for most software engineers. By far, UNIX system internals and networking (Layer 1 to Layer 3) expertise are the two most common types of alternate technical skills we seek.

50%至60%的SRE团队成员是谷歌软件工程师，更准确地说，是通过谷歌软件工程师的标准招聘程序招聘的人员。其余的40%至50%是非常接近谷歌软件工程师资格的候选人（即，具有所需技能集的85%至99%），并且除此之外，还拥有一组对SRE有用但对大多数软件工程师来说很少见的技术技能。远远来说，UNIX系统内部和网络（第1层至第3层）专业知识是我们寻求的两种最常见的替代技术技能。

Common to all SREs is the belief in and aptitude for developing software systems to solve complex problems. Within SRE, we track the career progress of both groups closely, and have to date found no practical difference in performance between engineers from the two tracks. In fact, the somewhat diverse background of the SRE team frequently results in clever, high-quality systems that are clearly the product of the synthesis of several skill sets.

SRE所有成员都相信并有能力开发软件系统来解决复杂的问题。在SRE中，我们密切跟踪两个团队的职业发展，并迄今为止发现两个团队之间的绩效没有实际区别。实际上，SRE团队的多样化背景经常产生智能而高质量的系统，这些系统显然是几种技能的综合产物。

The result of our approach to hiring for SRE is that we end up with a team of people who (a) will quickly become bored by performing tasks by hand, and (b) have the skill set necessary to write software to replace their previously manual work, even when the solution is complicated. SREs also end up sharing academic and intellectual background with the rest of the development organization. Therefore, SRE is fundamentally doing work that has historically been done by an operations team, but using engineers with software expertise, and banking on the fact that these engineers are inherently both predisposed to, and have the ability to, design and implement automation with software to replace human labor.

我们招聘SRE的方法的结果是，我们拥有一支由这样的人组成的团队：(a)很快就会对手动执行任务感到无聊，(b)拥有编写软件以替代以前的手动工作所需的技能集，即使解决方案很复杂。SRE还与其他开发组织共享学术和智力背景。因此，SRE从根本上做的是曾经由运维团队完成的工作，但使用拥有软件专业知识的工程师，并依靠这些工程师倾向于设计和实施用软件替代人力的自动化工作的事实。

By design, it is crucial that SRE teams are focused on engineering. Without constant engineering, operations load increases and teams will need more people just to keep pace with the workload. Eventually, a traditional ops-focused group scales linearly with service size: if the products supported by the service succeed, the operational load will grow with traffic. That means hiring more people to do the same tasks over and over again.

按照设计，SRE团队专注于工程方面非常重要。如果没有不断的工程工作，运维负担将增加，团队将需要更多的人员来跟上工作量。最终，一个传统的运维团队将与服务规模呈线性比例增长：如果被服务支持的产品获得成功，那么运维负担将随着流量的增长而增加。这意味着要雇用更多的人员来重复相同的任务。

To avoid this fate, the team tasked with managing a service needs to code or it will drown. Therefore, Google places a 50% cap on the aggregate “ops” work for all SREs— tickets, on-call, manual tasks, etc. This cap ensures that the SRE team has enough time in their schedule to make the service stable and operable. This cap is an upper bound; over time, left to their own devices, the SRE team should end up with very little operational load and almost entirely engage in development tasks, because the service basically runs and repairs itself: we want systems that are automatic, not just automated. In practice, scale and new features keep SREs on their toes.

为了避免这种命运，负责管理服务的团队需要编写代码，否则就会被任务量淹没。因此，谷歌对所有SRE的“ops”工作设定了50％的上限-包括工单、on-call、手动任务等。这个上限确保SRE团队有足够的时间来使服务稳定和可操作。这个上限是一个上限；随着时间的推移，SRE团队应该会几乎不承担运维任务，并主要从事开发任务，因为服务基本上是自行运行和维护的：我们希望的是自动化的系统，而不仅仅是自动化的。实际上，规模和新特性使SRE们保持紧张。

Google’s rule of thumb is that an SRE team must spend the remaining 50% of its time actually doing development. So how do we enforce that threshold? In the first place, we have to measure how SRE time is spent. With that measurement in hand, we ensure that the teams consistently spending less than 50% of their time on development work change their practices. Often this means shifting some of the operations burden back to the development team, or adding staff to the team without assigning that team additional operational responsibilities. Consciously maintaining this balance between ops and development work allows us to ensure that SREs have the bandwidth to engage in creative, autonomous engineering, while still retaining the wisdom gleaned from the operations side of running a service.

Google的经验法则是，一个SRE团队必须花费其余50％的时间来实际进行开发工作。那么我们如何执行这个门槛呢？首先，我们必须测算SRE团队的时间如何花费。有了这个测算结果，我们确保那些始终少于50％的时间用于开发工作的团队改变其做法。通常这意味着将一些运维负担转移到开发团队，或者增加团队的人员，而不给该团队分配额外的运维职责。有意识地保持运维和开发工作之间的平衡，使我们能够确保SRE有时间参与创造性的自主工程，同时仍然保留从运维方面运行服务所获得的智慧。

We’ve found that Google SRE’s approach to running large-scale systems has many advantages. Because SREs are directly modifying code in their pursuit of making Google’s systems run themselves, SRE teams are characterized by both rapid innovation and a large acceptance of change. Such teams are relatively inexpensive—supporting the same service with an ops-oriented team would require a significantly larger number of people. Instead, the number of SREs needed to run, maintain, and improve a system scales sublinearly with the size of the system. Finally, not only does SRE circumvent the dysfunctionality of the dev/ops split, but this structure also improves our product development teams: easy transfers between product development and SRE teams cross-train the entire group, and improve skills of developers who otherwise may have difficulty learning how to build a million-core distributed system.

我们发现，Google SRE运行大规模系统的方法具有许多优点。因为SRE直接修改代码以使Google的系统自我运行，所以SRE团队具有快速创新和大规模变革的特点。这样的团队相对来说成本较低，用一个运维团队来支持同一个服务需要更多的人力。相反，运行、维护和改进系统所需的SRE人数与系统的规模呈次线性关系。最后，SRE不仅规避了开发/运维分裂的功能障碍，而且这种结构还改进了我们的产品开发团队：产品开发和SRE团队之间的易于转移促进了整个团队的交叉培训，并提高了开发人员的技能，否则这些开发人员可能难以学习如何构建一个百万核心的分布式系统。

Despite these net gains, the SRE model is characterized by its own distinct set of challenges. One continual challenge Google faces is hiring SREs: not only does SRE compete for the same candidates as the product development hiring pipeline, but the fact that we set the hiring bar so high in terms of both coding and system engineering skills means that our hiring pool is necessarily small. As our discipline is relatively new and unique, not much industry information exists on how to build and manage an SRE team (although hopefully this book will make strides in that direction!). And once an SRE team is in place, their potentially unorthodox approaches to service management require strong management support. For example, the decision to stop releases for the remainder of the quarter once an error budget is depleted might not be embraced by a product development team unless mandated by their management.

尽管有这些净收益，SRE模型仍面临着一系列独特的挑战。Google面临的一个持续挑战是聘请SRE：不仅SRE要与产品开发招聘渠道争夺同样的候选人，而且我们在编码和系统工程技能方面设置的高招聘门槛意味着我们的招聘池必然很小。由于我们的学科相对较新且独特，因此在如何构建和管理SRE团队方面没有太多行业信息（尽管希望本书可以在这方面取得进展！）。一旦建立了SRE团队，他们可能对服务管理采取非传统方法，需要得到强有力的管理支持。例如，一旦错误预算用完，停止发布的决定可能不会得到产品开发团队的支持，除非他们的管理层强制执行。

<br>

---

**[Back to contents of the chapter（返回章节目录）](introduction.md)**

- **Previous Section（上一节）:[The Sysadmin Approach to Service Management（系统管理员的服务管理方法）](the_sysadmin_approach_to_service_management.md)**
- **Next Section（下一节）：[Tenets of SRE（SRE的原则）](tenets_of_sre.md)**
