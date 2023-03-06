## **Tenets of SRE**

## **SRE的原则**

> The term “DevOps” emerged in industry in late 2008 and as of this writing (early 2016) is still in a state of flux. Its core principles—involvement of the IT function in each phase of a system’s design and development, heavy reliance on automation versus human effort, the application of engineering practices and tools to operations tasks—are consistent with many of SRE’s principles and practices. One could view DevOps as a generalization of several core SRE principles to a wider range of organizations, management structures, and personnel. One could equivalently view SRE as a specific implementation of DevOps with some idiosyncratic extensions.
>
> “DevOps”这个术语于2008年末出现在行业中，截至本文撰写（2016年初），它仍处于变化中。它的核心原则——将IT功能纳入系统设计和开发的每个阶段，重度依赖自动化而非人力，将工程实践和工具应用于运维任务——与SRE的许多原则和实践相一致。人们可以将DevOps视为将几个核心SRE原则泛化到更广泛的组织、管理结构和人员范围的一种方法，也可以等价地将SRE视为对DevOps的一种具体实现，其中有一些特殊的扩展。

While the nuances of workflows, priorities, and day-to-day operations vary from SRE team to SRE team, all share a set of basic responsibilities for the service(s) they support, and adhere to the same core tenets. In general, an SRE team is responsible for the availability, latency, performance, efficiency, change management, monitoring, emergency response, and capacity planning of their service(s). We have codified rules of engagement and principles for how SRE teams interact with their environment— not only the production environment, but also the product development teams, the testing teams, the users, and so on. Those rules and work practices help us to main‐ tain our focus on engineering work, as opposed to operations work.

虽然SRE团队之间的工作流程、优先级和日常操作的细节有所不同，但所有团队都有一组基本的责任来支持他们所支持的服务，并遵守相同的核心原则。通常，SRE团队负责他们所支持的服务的可用性、延迟、性能、效率、变更管理、监控、紧急响应和容量规划。我们已经制定了与他们的环境互动的原则和规则，不仅是生产环境，还包括产品开发团队、测试团队、用户等。这些规则和工作实践帮助我们保持对工程工作的关注，而不是对运维工作的关注。

The following section discusses each of the core tenets of Google SRE.

下面的章节将讨论Google SRE的每一个核心原则。

### **Ensuring a Durable Focus on Engineering**

### **确保持续关注工程方面**

As already discussed, Google caps operational work for SREs at 50% of their time. Their remaining time should be spent using their coding skills on project work. In practice, this is accomplished by monitoring the amount of operational work being done by SREs, and redirecting excess operational work to the product development teams: reassigning bugs and tickets to development managers, [re]integrating developers into on-call pager rotations, and so on. The redirection ends when the operational load drops back to 50% or lower. This also provides an effective feedback mechanism, guiding developers to build systems that don’t need manual intervention. This approach works well when the entire organization—SRE and development alike —understands why the safety valve mechanism exists, and supports the goal of having no overflow events because the product doesn’t generate enough operational load to require it.
