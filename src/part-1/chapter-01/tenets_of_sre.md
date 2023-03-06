## **Tenets of SRE**

## **SRE的原则**

> The term “DevOps” emerged in industry in late 2008 and as of this writing (early 2016) is still in a state of flux. Its core principles—involvement of the IT function in each phase of a system’s design and development, heavy reliance on automation versus human effort, the application of engineering practices and tools to operations tasks—are consistent with many of SRE’s principles and practices. One could view DevOps as a generalization of several core SRE principles to a wider range of organizations, management structures, and personnel. One could equivalently view SRE as a specific implementation of DevOps with some idiosyncratic extensions.
>
> “DevOps”这个术语于2008年末出现在行业中，截至本文撰写（2016年初），它仍处于变化中。它的核心原则——将IT功能纳入系统设计和开发的每个阶段，重度依赖自动化而非人力，将工程实践和工具应用于运维任务——与SRE的许多原则和实践相一致。人们可以将DevOps视为将几个核心SRE原则泛化到更广泛的组织、管理结构和人员范围的一种方法，也可以等价地将SRE视为对DevOps的一种具体实现，其中有一些特殊的扩展。

While the nuances of workflows, priorities, and day-to-day operations vary from SRE team to SRE team, all share a set of basic responsibilities for the service(s) they support, and adhere to the same core tenets. In general, an SRE team is responsible for the availability, latency, performance, efficiency, change management, monitoring, emergency response, and capacity planning of their service(s). We have codified rules of engagement and principles for how SRE teams interact with their environment— not only the production environment, but also the product development teams, the testing teams, the users, and so on. Those rules and work practices help us to maintain our focus on engineering work, as opposed to operations work.

虽然SRE团队之间的工作流程、优先级和日常操作的细节有所不同，但所有团队都有一组基本的责任来支持他们所支持的服务，并遵守相同的核心原则。通常，SRE团队负责他们所支持的服务的可用性、延迟、性能、效率、变更管理、监控、紧急响应和容量规划。我们已经制定了与他们的环境互动的原则和规则，不仅是生产环境，还包括产品开发团队、测试团队、用户等。这些规则和工作实践帮助我们保持对工程工作的关注，而不是对运维工作的关注。

The following section discusses each of the core tenets of Google SRE.

下面的章节将讨论Google SRE的每一个核心原则。

<br>

### **Ensuring a Durable Focus on Engineering**

### **确保持续关注工程方面**

As already discussed, Google caps operational work for SREs at 50% of their time. Their remaining time should be spent using their coding skills on project work. In practice, this is accomplished by monitoring the amount of operational work being done by SREs, and redirecting excess operational work to the product development teams: reassigning bugs and tickets to development managers, [re]integrating developers into on-call pager rotations, and so on. The redirection ends when the operational load drops back to 50% or lower. This also provides an effective feedback mechanism, guiding developers to build systems that don’t need manual intervention. This approach works well when the entire organization—SRE and development alike —understands why the safety valve mechanism exists, and supports the goal of having no overflow events because the product doesn’t generate enough operational load to require it.

正如前面讨论的，Google将SRE的运维工作限制在他们50%的时间内。他们剩下的时间应该用于项目工作，利用他们的编码技能。在实践中，这是通过监控SRE的运维工作量，并将多余的运维工作重新分配给产品开发团队来实现的：将漏洞和工单重新分配给开发经理，将开发人员重新纳入on-call值班轮换等等。当运维负载降至50％或更低时，重新分配工作就会停止。这也提供了一种有效的反馈机制，指导开发人员构建不需要手动干预的系统。当整个组织（包括SRE和开发团队）都理解安全阀机制的存在原因，并支持达成不需要超负荷事件的目标，因为产品不会产生足够的运维负荷来要求这一点时，这种方法非常有效。

When they are focused on operations work, on average, SREs should receive a maximum of two events per 8–12-hour on-call shift. This target volume gives the on-call engineer enough time to handle the event accurately and quickly, clean up and restore normal service, and then conduct a postmortem. If more than two events occur regularly per on-call shift, problems can’t be investigated thoroughly and engineers are sufficiently overwhelmed to prevent them from learning from these events. A scenario of pager fatigue also won’t improve with scale. Conversely, if on-call SREs consistently receive fewer than one event per shift, keeping them on point is a waste of their time.

当SRE专注于运维工作时，平均而言，每8-12小时的值班时间内，他们应该最多接收两个事件。这个目标数量给予值班工程师足够的时间来准确快速地处理事件，恢复正常服务，然后进行事后审查。如果每个值班时间内经常发生超过两个事件，问题就无法得到彻底的调查，工程师也会感到不堪重负，无法从这些事件中学习。同时，如果值班的SRE每次都只接收到少于一个事件，那么让他们值班是浪费他们的时间。

Postmortems should be written for all significant incidents, regardless of whether or not they paged; postmortems that did not trigger a page are even more valuable, as they likely point to clear monitoring gaps. This investigation should establish what happened in detail, find all root causes of the event, and assign actions to correct the problem or improve how it is addressed next time. Google operates under a blame- free postmortem culture, with the goal of exposing faults and applying engineering to fix these faults, rather than avoiding or minimizing them.

所有重大事件都应编写事故调查报告，无论是否已解决; 没有触发警报的后期报告更有价值，因为它们可能指出明显的监控漏洞。此调查应详细说明发生了什么，找到事件的所有根本原因，并指定纠正问题或改进下一次解决问题的操作。 Google实行无过错事故调查文化，旨在暴露故障并应用工程学来修复这些故障，而不是避免或最小化它们。

<br>

### **Pursuing Maximum Change Velocity Without Violating a Service’s SLO**

### **追求最大的变更速率而不违反服务的SLO**

Product development and SRE teams can enjoy a productive working relationship by eliminating the structural conflict in their respective goals. The structural conflict is between pace of innovation and product stability, and as described earlier, this conflict often is expressed indirectly. In SRE we bring this conflict to the fore, and then resolve it with the introduction of an error budget.

产品开发和SRE团队可以通过消除它们各自目标之间的结构性冲突来建立一种有效的工作关系。这种结构性冲突是创新速度和产品稳定性之间的冲突，正如前面所描述的，这种冲突通常是间接表达的。在SRE中，我们将这种冲突暴露出来，然后通过引入错误预算来解决它。

The error budget stems from the observation that 100% is the wrong reliability target for basically everything (pacemakers and anti-lock brakes being notable exceptions). In general, for any software service or system, 100% is not the right reliability target because no user can tell the difference between a system being 100% available and 99.999% available. There are many other systems in the path between user and service (their laptop, their home WiFi, their ISP, the power grid...) and those systems collectively are far less than 99.999% available. Thus, the marginal difference between 99.999% and 100% gets lost in the noise of other unavailability, and the user receives no benefit from the enormous effort required to add that last 0.001% of availability.

错误预算来源于以下观察：100%的可靠性目标基本上是所有事物的错误目标（起搏器和防抱死制动系统是值得注意的例外）。通常情况下，对于任何软件服务或系统，100%的可靠性目标都不是正确的目标，因为没有用户能够区分系统的可用性是100%还是99.999%。在用户和服务之间还有许多其他系统（例如他们的笔记本电脑、家庭 WiFi、ISP、电网等），这些系统的可用性总体远低于99.999%。因此，99.999%和100%之间的微小差别会淹没在其他不可用性的噪音中，用户无法从花费大量精力增加最后的0.001%的可用性中获得任何好处。

If 100% is the wrong reliability target for a system, what, then, is the right reliability target for the system? This actually isn’t a technical question at all—it’s a product question, which should take the following considerations into account:

* What level of availability will the users be happy with, given how they use the product?
* What alternatives are available to users who are dissatisfied with the product’s availability?
* What happens to users’ usage of the product at different availability levels?

如果100%是系统的错误可靠性目标，那么什么才是系统的正确可靠性目标呢？实际上，这根本不是一个技术问题，而是一个产品问题，应该考虑以下因素：

* 用户将对什么水平的可用性感到满意，考虑到他们如何使用该产品？
* 什么样的替代方案可供对产品可用性不满意的用户选择？
* 不同的可用性水平会对用户对产品的使用产生什么影响？

The business or the product must establish the system’s availability target. Once that target is established, the error budget is one minus the availability target. A service that’s 99.99% available is 0.01% unavailable. That permitted 0.01% unavailability is the service’s error budget. We can spend the budget on anything we want, as long as we don’t overspend it.

一旦系统的可用性目标确定，业务或产品就必须设立错误预算。错误预算等于1减去可用性目标。例如，一个可用性为99.99%的服务，就有0.01%不可用。这个0.01%不可用即是该服务的错误预算。我们可以将预算用在任何需要的地方，只要不超支即可。

So how do we want to spend the error budget? The development team wants to launch features and attract new users. Ideally, we would spend all of our error budget taking risks with things we launch in order to launch them quickly. This basic premise describes the whole model of error budgets. As soon as SRE activities are conceptualized in this framework, freeing up the error budget through tactics such as phased rollouts and 1% experiments can optimize for quicker launches.

因此，我们想如何花费错误预算？开发团队希望推出新功能并吸引新用户。理想情况下，我们会花费所有错误预算冒险尝试推出新功能，以便尽快推出它们。这个基本前提描述了整个错误预算模型。一旦将SRE活动概念化为这种框架，通过分阶段发布和1%实验等策略释放错误预算，可以优化快速发布的目标。

> 1% experiments是指通过在小规模用户群体中测试新功能或改进，以评估其效果和可靠性。通常情况下，这些实验仅在一小部分用户中进行，通常为1%的用户，以确保新功能或改进不会对整个系统或大多数用户造成不良影响。

The use of an error budget resolves the structural conflict of incentives between development and SRE. SRE’s goal is no longer “zero outages”; rather, SREs and product developers aim to spend the error budget getting maximum feature velocity. This change makes all the difference. An outage is no longer a “bad” thing—it is an expected part of the process of innovation, and an occurrence that both development and SRE teams manage rather than fear.

使用错误预算解决了开发和SRE之间的结构性冲突。SRE的目标不再是“零故障”，而是SRE和产品开发人员旨在利用错误预算实现最大功能发布速度。这种变化产生了很大的影响。故障不再是一件“坏事”，它是创新过程中预期发生的一部分，是开发和SRE团队管理而不是害怕的事件。

<br>

### **Monitoring**

### **监控**

Monitoring is one of the primary means by which service owners keep track of a system’s health and availability. As such, monitoring strategy should be constructed thoughtfully. A classic and common approach to monitoring is to watch for a specific value or condition, and then to trigger an email alert when that value is exceeded or that condition occurs. However, this type of email alerting is not an effective solution: a system that requires a human to read an email and decide whether or not some type of action needs to be taken in response is fundamentally flawed. Monitoring should never require a human to interpret any part of the alerting domain. Instead, software should do the interpreting, and humans should be notified only when they need to take action.

监控是服务所有者跟踪系统健康状况和可用性的主要手段之一。因此，监控策略应该经过深思熟虑地构建。一种经典且常见的监控方法是观察特定的值或条件，然后在超过该值或出现该条件时触发电子邮件警报。然而，这种类型的电子邮件警报并不是有效的解决方案：需要人工阅读电子邮件并决定是否需要采取某种形式的行动来响应的系统从根本上存在缺陷。监控不应该需要人类解释警报领域的任何部分。相反，软件应该进行解释，只有在需要采取行动时才应通知人类。

There are three kinds of valid monitoring output:

* Alerts: Signify that a human needs to take action immediately in response to something that is either happening or about to happen, in order to improve the situation.
* Tickets: Signify that a human needs to take action, but not immediately. The system cannot automatically handle the situation, but if a human takes action in a few days, no damage will result.
* Logging: No one needs to look at this information, but it is recorded for diagnostic or forensic purposes. The expectation is that no one reads logs unless something else prompts them to do so.

有三种有效的监控输出：

* Alerts：表示需要立即采取行动以改善情况，因为某些事情正在发生或即将发生。
* Tickets：意味着需要人类采取行动，但不需要立即采取。系统无法自动处理该情况，但如果人类在几天内采取行动，就不会造成任何损害。
* Logging：不需要任何人查看这些信息，但它们被记录下来用于诊断或取证目的。期望是，除非有其他原因促使他们这样做，否则没有人会阅读日志。

<br>

### **Emergency Response**

### **应急响应**

Reliability is a function of mean time to failure (MTTF) and mean time to repair (MTTR). The most relevant metric in evaluating the effectiveness of emergency response is how quickly the response team can bring the system back to health —that is, the MTTR.

可靠性是平均故障时间（MTTF）和平均修复时间（MTTR）的函数。在评估应急响应的有效性时，最相关的指标是响应团队将系统恢复正常所需的时间，即MTTR。

Humans add latency. Even if a given system experiences more actual failures, a system that can avoid emergencies that require human intervention will have higher availability than a system that requires hands-on intervention. When humans are necessary, we have found that thinking through and recording the best practices ahead of time in a “playbook” produces roughly a 3x improvement in MTTR as compared to the strategy of “winging it.” The hero jack-of-all-trades on-call engineer does work, but the practiced on-call engineer armed with a playbook works much better. While no playbook, no matter how comprehensive it may be, is a substitute for smart engineers able to think on the fly, clear and thorough troubleshooting steps and tips are valuable when responding to a high-stakes or time-sensitive page. Thus, Google SRE relies on on-call playbooks, in addition to exercises such as the “Wheel of Misfortune,”2 to prepare engineers to react to on-call events.

人类会增加延迟。即使一个系统经历更多实际故障，但一个能够避免需要人类干预的紧急情况的系统，其可用性将比需要人工干预的系统更高。当需要人类干预时，我们发现提前思考和记录最佳实践并编制“playbook”比即兴应对策略可以将MTTR提高大约三倍。超级万能的值班工程师可能是有效的，但拥有playbook的训练有素的值班工程师效果更好。虽然没有多么全面的playbook能够替代能够在现场即兴思考的聪明工程师，但清晰、详尽的故障排除步骤和提示在应对高风险或时间敏感的页面时是非常有价值的。因此，Google SRE依靠值班playbook以及像“Wheel of Misfortune”这样的练习，为工程师准备应对值班事件。

> 在SRE的实践中，playbook被广泛应用于处理各种紧急事件，例如系统崩溃、网络故障等，以及日常维护任务，例如更新软件、更换硬件等。playbook中通常包含详细的检查列表、诊断步骤、修复步骤和故障排除技巧，可以指导人们在出现问题时快速定位问题并采取适当的行动。
>
> "Wheel of Misfortune" 是一种SRE练习，旨在帮助工程师在应对各种紧急情况时更好地思考和合作。在这个练习中，参与者会分成多个小组，每个小组会被分配一个场景，例如“数据库故障”或“网络瓶颈”。然后，每个小组会通过旋转“不幸之轮”来决定在该场景下他们需要面对的额外挑战，例如“在紧急情况下，其中一个组员临时离开”或“你必须与一个刚刚入职的新人一起解决问题”。这样的练习可以让工程师更好地理解在高压情况下如何更好地工作，并提高他们应对各种突发情况的能力。

<br>

### **Change Management**

### **变更管理**

SRE has found that roughly 70% of outages are due to changes in a live system. Best practices in this domain use automation to accomplish the following:

* Implementing progressive rollouts
* Quickly and accurately detecting problems
* Rolling back changes safely when problems arise

SRE发现，大约70%的系统故障是由于系统的变更导致的。在这个领域的最佳实践使用自动化来实现以下目标：

* 实现渐进式发布
* 快速而准确地检测问题
* 当出现问题时安全回滚变更

This trio of practices effectively minimizes the aggregate number of users and operations exposed to bad changes. By removing humans from the loop, these practices avoid the normal problems of fatigue, familiarity/contempt, and inattention to highly repetitive tasks. As a result, both release velocity and safety increase.

这三种实践有效地将暴露于错误变更的用户和操作数量最小化。通过从环节中排除人类行为，这些实践避免了疲劳、习惯/轻视和对高度重复任务的忽视等常见问题。因此，发布速度和安全性都得到提高。

<br>

### **Demand Forecasting and Capacity Planning**

### **需求预测和容量规划**

Demand forecasting and capacity planning can be viewed as ensuring that there is sufficient capacity and redundancy to serve projected future demand with the required availability. There’s nothing particularly special about these concepts, except that a surprising number of services and teams don’t take the steps necessary to ensure that the required capacity is in place by the time it is needed. Capacity planning should take both organic growth (which stems from natural product adoption and usage by customers) and inorganic growth (which results from events like feature launches, marketing campaigns, or other business-driven changes) into account.

需求预测和容量规划可被视为确保在所需可用性的情况下有足够的容量和冗余来满足预期未来的需求。这些概念并没有什么特别之处，只是令人惊讶的是，很多服务和团队没有采取必要的步骤，确保所需的容量在需要时已经到位。容量规划应该考虑到有机增长（源于自然产品被客户采用和使用）和非有机增长（源于功能发布、营销活动或其他业务驱动变化等事件）两个方面。

Several steps are mandatory in capacity planning:

* An accurate organic demand forecast, which extends beyond the lead time required for acquiring capacity
* An accurate incorporation of inorganic demand sources into the demand forecast
* Regular load testing of the system to correlate raw capacity (servers, disks, and so on) to service capacity

以下几个步骤在容量规划中是必要的：

* 一个准确的有机需求预测，需要超出获取容量所需的前置时间
* 将无机需求来源准确纳入需求预测中
* 定期负载测试系统，以将原始容量（服务器、磁盘等）与服务容量相对应

Because capacity is critical to availability, it naturally follows that the SRE team must be in charge of capacity planning, which means they also must be in charge of provisioning.

由于容量对可用性至关重要，自然而然地，SRE团队必须负责容量规划，这意味着他们也必须负责供应。

<br>

### **Provisioning**

### **供应管理**

Provisioning combines both change management and capacity planning. In our experience, provisioning must be conducted quickly and only when necessary, as capacity is expensive. This exercise must also be done correctly or capacity doesn’t work when needed. Adding new capacity often involves spinning up a new instance or location, making significant modification to existing systems (configuration files, load balancers, networking), and validating that the new capacity performs and delivers correct results. Thus, it is a riskier operation than load shifting, which is often done multiple times per hour, and must be treated with a corresponding degree of extra caution.

供应管理是改变管理和容量规划的结合体。根据我们的经验，供应管理必须快速进行，只有在必要时才进行，因为容量很昂贵。这项工作必须正确进行，否则在需要时容量将无法使用。增加新的容量通常涉及启动新实例或位置，对现有系统进行重大修改（配置文件、负载均衡器、网络），并验证新容量的性能和正确结果的提供。因此，这是一个比负载转移更具风险的操作，后者通常每小时进行多次，并且必须额外谨慎对待。

<br>

### **Efficiency and Performance**

### **效率和性能表现**

Efficient use of resources is important any time a service cares about money. Because SRE ultimately controls provisioning, it must also be involved in any work on utilization, as utilization is a function of how a given service works and how it is provisioned. It follows that paying close attention to the provisioning strategy for a service, and therefore its utilization, provides a very, very big lever on the service’s total costs.

高效使用资源在任何服务关心成本的时候都非常重要。因为SRE最终控制着供应，所以它必须参与任何关于利用率的工作，因为利用率是一个给定服务工作方式和供应方式的函数。因此，密切关注服务的供应策略和其利用率，可以对服务的总成本产生非常大的影响。

Resource use is a function of demand (load), capacity, and software efficiency. SREs predict demand, provision capacity, and can modify the software. These three factors are a large part (though not the entirety) of a service’s efficiency.

资源使用是需求（负载）、容量和软件效率的函数。SRE负责预测需求、提供容量并可以修改软件。这三个因素是服务效率的重要组成部分（尽管不是全部）。

Software systems become slower as load is added to them. A slowdown in a service equates to a loss of capacity. At some point, a slowing system stops serving, which corresponds to infinite slowness. SREs provision to meet a capacity target at a specific response speed, and thus are keenly interested in a service’s performance. SREs and product developers will (and should) monitor and modify a service to improve its performance, thus adding capacity and improving efficiency.

随着负载的增加，软件系统变得越来越慢。服务的减速等同于容量的损失。在某个时刻，系统的减速将停止服务，这对应于无限减速。SRE会根据特定响应速度的容量目标进行配置，因此对服务的性能非常关注。SRE和产品开发人员将（也应该）监测和修改服务以提高其性能，从而增加容量并提高效率。

<br>

---

**[Back to contents of the chapter（返回章节目录）](introduction.md)**

* **Previous Section（上一节）:[Google’s Approach to Service Management:Site Reliability Engineering（谷歌的服务管理方法：SRE）](google's_approach_to_service_management_site_reliability_engineering.md)**
* **Next Section（下一节）：[The End of the Beginning（本章结语）](the_end_of_the_beginning.md)**
