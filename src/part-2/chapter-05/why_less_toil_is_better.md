## **Why Less Toil Is Better**

## **为什么更少的劳作更好**

Our SRE organization has an advertised goal of keeping operational work (i.e., toil) below 50% of each SRE’s time. At least 50% of each SRE’s time should be spent on engineering project work that will either reduce future toil or add service features. Feature development typically focuses on improving reliability, performance, or utilization, which often reduces toil as a second-order effect.

我们的SRE组织有一个公开的目标，即把运维工作（即劳作）保持在每个SRE的时间的50%以下。每个SRE至少有50%的时间应该花在工程项目工作上，这将减少未来的劳作或增加服务功能。功能开发通常侧重于改善可靠性、性能或利用率，这通常作为第二阶效应减少劳作。

We share this 50% goal because toil tends to expand if left unchecked and can quickly fill 100% of everyone’s time. The work of reducing toil and scaling up services is the "Engineering" in Site Reliability Engineering. Engineering work is what enables the SRE organization to scale up sublinearly with service size and to manage services more efficiently than either a pure Dev team or a pure Ops team.

我们分享这个50%的目标，因为如果不加控制，劳作往往会扩大，并会迅速填满每个人的100%的时间。减少劳作和扩大服务规模的工作是SRE中的 "工程"。工程工作是使SRE组织能够随着服务规模的扩大而呈次线性增长，并比纯开发团队或纯运维团队更有效地管理服务。

Furthermore, when we hire new SREs, we promise them that SRE is not a typical Ops organization, quoting the 50% rule just mentioned. We need to keep that promise by not allowing the SRE organization or any subteam within it to devolve into an Ops team.

此外，当我们雇用新的SRE时，我们向他们承诺，SRE不是一个典型的Ops组织，引用刚才提到的50%的规则。我们需要遵守这个承诺，不允许SRE组织或其中的任何子团队演变成一个运维团队。

### **Calculating Toil**

### **计算劳作**

If we seek to cap the time an SRE spends on toil to 50%, how is that time spent?

如果我们寻求将一个SRE花在劳作上的时间限制在50%，那么这些时间是如何度过的？

There’s a floor on the amount of toil any SRE has to handle if they are on-call. A typical SRE has one week of primary on-call and one week of secondary on-call in each cycle (for discussion of primary versus secondary on-call shifts, see Chapter 11). It follows that in a 6-person rotation, at least 2 of every 6 weeks are dedicated to on-call shifts and interrupt handling, which means the lower bound on potential toil is 2/6 = 33% of an SRE’s time. In an 8-person rotation, the lower bound is 2/8 = 25%.

任何SRE在待命的情况下都要处理一定的工作量。一个典型的SRE在每个周期有一周的主要值班和一周的次要值班（关于主要值班和次要值班的讨论，见第11章）。因此，在一个6人的轮换中，每6周中至少有2周用于待命和处理中断，这意味着潜在的劳作的下限是2/6=33%的SRE时间。在8人的轮换中，下限是2/8=25%。

Consistent with this data, SREs report that their top source of toil is interrupts (that is, non-urgent service-related messages and emails). The next leading source is on-call (urgent) response, followed by releases and pushes. Even though our release and push processes are usually handled with a fair amount of automation, there’s still plenty of room for improvement in this area.

与此数据一致，SREs报告说他们最主要的工作来源是中断（即非紧急的服务相关信息和电子邮件）。下一个主要来源是待命（紧急）响应，其次是发布和推送。尽管我们的发布和推送流程通常都有相当程度的自动化处理，但在这个领域仍有很大的改进空间。

Quarterly surveys of Google’s SREs show that the average time spent toiling is about 33%, so we do much better than our overall target of 50%. However, the average doesn’t capture outliers: some SREs claim 0% toil (pure development projects with no on-call work) and others claim 80% toil. When individual SREs report excessive toil, it often indicates a need for managers to spread the toil load more evenly across the team and to encourage those SREs to find satisfying engineering projects.

对谷歌SRE的季度调查显示，平均花在劳作上的时间约为33%，所以我们比50%的总体目标要好得多。然而，平均数并没有捕捉到异常情况：一些SRE声称0%的劳作（纯粹的开发项目，没有随叫随到的工作），另一些则声称80%的劳作。当个别的SRE报告了过多的劳作时，这往往表明管理者需要在团队中更均匀地分配劳作负担，并鼓励这些SRE找到令人满意的工程项目。

<br>

---

**[Back to contents of the chapter（返回章节目录）](eliminating_toil.md)**

* **Previous Section（上一节）：[Toil Defined（劳作的定义）](toil_defined.md)**
* **Next Section（下一节）：[What Qualifies as Engineering?（什么符合工程的标准）](what_qualifies_as_engineering.md)**
