## **Measuring Service Risk**

## **衡量服务风险**

As standard practice at Google, we are often best served by identifying an objective metric to represent the property of a system we want to optimize. By setting a target, we can assess our current performance and track improvements or degradations over time. For service risk, it is not immediately clear how to reduce all of the potential factors into a single metric. Service failures can have many potential effects, including user dissatisfaction, harm, or loss of trust; direct or indirect revenue loss; brand or reputational impact; and undesirable press coverage. Clearly, some of these factors are very hard to measure. To make this problem tractable and consistent across many types of systems we run, we focus on unplanned downtime.

作为Google的标准做法，我们通常通过确定一个客观指标来表示我们想要优化的系统属性。通过设定目标，我们可以评估当前的表现，并跟踪随时间改进或恶化的情况。对于服务风险，如何将所有可能的因素减少到一个单一指标并不是容易做到的。服务故障可能会产生许多潜在影响，包括用户不满意、损害或失去信任；直接或间接的收入损失；品牌或声誉影响；以及不良新闻报道。显然，其中一些因素很难衡量。为了使这个问题在我们运行的许多类型的系统中可控和一致，我们专注于非计划停机时间。

For most services, the most straightforward way of representing risk tolerance is in terms of the acceptable level of unplanned downtime. Unplanned downtime is captured by the desired level of service availability, usually expressed in terms of the number of “nines” we would like to provide: 99.9%, 99.99%, or 99.999% availability. Each additional nine corresponds to an order of magnitude improvement toward 100% availability. For serving systems, this metric is traditionally calculated based on the proportion of system uptime (see Equation 3-1).

对于大多数服务来说，表示风险容忍度的最直接方式是以可接受的非计划停机水平为基础。非计划停机由所需的服务可用性水平捕获，通常以我们希望提供的“9”数来表达：99.9%、99.99%或99.999%的可用性。每增加一个9，就相当于朝着100%可用性提高一个数量级。对于服务系统，这个指标通常基于系统正常运行时间的比例来计算（见Equation 3-1）。

$$availability = \frac{uptime}{uptime + downtime}$$
> Equation 3-1. Time-based availability

Using this formula over the period of a year, we can calculate the acceptable number of minutes of downtime to reach a given number of nines of availability. For example, a system with an availability target of 99.99% can be down for up to 52.56 minutes in a year and stay within its availability target; see [Appendix A](./../../appendix/appendix_a_availability_table.md) for a table.

使用这个公式，我们可以在一年内计算出达到给定可用性的“9”的数量所允许的宕机时间（以分钟为单位）。例如，一个可用性目标为99.99％的系统可以在一年内停机高达52.56分钟，并保持在其可用性目标范围内。详见[附录A](./../../appendix/appendix_a_availability_table.md)的表格。

At Google, however, a time-based metric for availability is usually not meaningful because we are looking across globally distributed services. Our approach to fault isolation makes it very likely that we are serving at least a subset of traffic for a given service somewhere in the world at any given time (i.e., we are at least partially “up” at all times). Therefore, instead of using metrics around uptime, we define availability in terms of the request success rate. Equation 3-2 shows how this yield-based metric is calculated over a rolling window (i.e., proportion of successful requests over a one-day window).

在Google，使用基于时间的可用性度量通常没有意义，因为我们从跨全球分布的服务进行考虑。我们的故障隔离方法使得在任何给定时间，在某个地方为给定服务提供了至少部分流量（即，我们始终在某种程度上“运行”）。因此，我们不使用关于正常运行时间的度量，而是根据请求成功率来定义可用性。Equation 3-2展示了如何在一个滑动窗口内（即一天的窗口内）计算此度量值（即成功请求的比例）。

$$availability = \frac{successful requests}{total requests}$$
> Equation 3-2. Aggregate availability

For example, a system that serves 2.5M requests in a day with a daily availability target of 99.99% can serve up to 250 errors and still hit its target for that given day.

例如，一天内服务250万请求的系统，如果每天的可用性目标为99.99％，那么可以出现最多250个错误。

In a typical application, not all requests are equal: failing a new user sign-up request is different from failing a request polling for new email in the background. In many cases, however, availability calculated as the request success rate over all requests is a reasonable approximation of unplanned downtime, as viewed from the end-user perspective.

在典型的应用程序中，并非所有请求都是等价的：失败的新用户注册请求与失败的后台新邮件轮询请求不同。然而，在许多情况下，从用户的角度来看，计算所有请求的请求成功率作为意外停机量的合理近似值也是合理的。

Quantifying unplanned downtime as a request success rate also makes this availability metric more amenable for use in systems that do not typically serve end users directly. Most nonserving systems (e.g., batch, pipeline, storage, and transactional systems) have a well-defined notion of successful and unsuccessful units of work. Indeed, while the systems discussed in this chapter are primarily consumer and infrastructure serving systems, many of the same principles also apply to nonserving systems with minimal modification.

将意外停机量化为请求成功率，还使得这种可用性指标更容易用于通常不直接为终端用户提供服务的系统。大多数非服务系统（例如批处理、管道、存储和事务系统）都有成功和失败工作单位的明确定义。实际上，虽然本章讨论的系统主要是面向消费者和基础设施服务系统，但许多相同的原则也适用于非服务系统，只需进行最少的修改即可。

For example, a batch process that extracts, transforms, and inserts the contents of one of our customer databases into a data warehouse to enable further analysis may be set to run periodically. Using a request success rate defined in terms of records successfully and unsuccessfully processed, we can calculate a useful availability metric despite the fact that the batch system does not run constantly.

例如，一个批处理进程，将我们一个客户数据库中的内容提取、转换并插入数据库以进行进一步的分析，可能被设置为定期运行。使用以成功和不成功处理的记录为定义的请求成功率，我们可以计算出一个有用的可用性度量，尽管批处理系统并不是一直在运行。

Most often, we set quarterly availability targets for a service and track our performance against those targets on a weekly, or even daily, basis. This strategy lets us manage the service to a high-level availability objective by looking for, tracking down, and fixing meaningful deviations as they inevitably arise. See Chapter 4 for more details.

大多数情况下，我们为一个服务设定季度可用性目标，并每周或甚至每天跟踪我们的表现。这种策略使我们能够通过寻找、跟踪和修复显著偏差，将服务管理到高水平的可用性目标。有关更多细节，请参见第四章。

<br>

---

**[Back to contents of the chapter（返回章节目录）](embracing_risk.md)**

* **Previous Section（上一节）：[Managing Risk（管理风险）](managing_risk.md)**
* **Next Section（下一节）：[Risk Tolerance of Services（服务的风险承受能力）](risk_tolerance_of_services.md)**
