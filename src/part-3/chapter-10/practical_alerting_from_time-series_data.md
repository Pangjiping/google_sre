# **Practical Alerting from Time-Series Data**

# **来自时间序列数据的实用警报**

> Written by Jamie Wilkinson
>
> Edited by Kavita Guliani

> May the queries flow, and the pager stay silent.
>
> —Traditional SRE blessing

Monitoring, the bottom layer of the Hierarchy of Production Needs, is fundamental to running a stable service. Monitoring enables service owners to make rational decisions about the impact of changes to the service, apply the scientific method to incident response, and of course ensure their reason for existence: to measure the service’s alignment with business goals (see [Chapter 6](../../part-2/chapter-06/monitoring_distributed_systems.md)).

监控是生产需求层次结构的底层，是运行稳定服务的基础。监控使服务所有者能够就服务变更的影响做出合理的决策，将科学方法应用于事件响应，当然还要确保它们存在的理由：衡量服务与业务目标的一致性（参见[第6章]((../../part-2/chapter-06/monitoring_distributed_systems.md))）。

Regardless of whether or not a service enjoys SRE support, it should be run in a symbiotic relationship with its monitoring. But having been tasked with ultimate responsibility for Google Production, SREs develop a particularly intimate knowledge of the monitoring infrastructure that supports their service.

无论服务是否有SRE支持，它都应该与其监控以共生关系运行。但是，由于承担了Google生产的最终责任，SRE对支持其服务的监控基础设施有了特别深入的了解。

Monitoring a very large system is challenging for a couple of reasons:

* The sheer number of components being analyzed
* The need to maintain a reasonably low maintenance burden on the engineers responsible for the system

出于以下几个原因，监控大型系统具有挑战性：

* 具有大量需要被分析的组件
* 保持负责系统的工程师合理的低维护负担

Google’s monitoring systems don’t just measure simple metrics, such as the average response time of an unladen European web server; we also need to understand the distribution of those response times across all web servers in that region. This knowledge enables us to identify the factors contributing to the latency tail.

Google的监控系统不仅仅测量简单的指标，例如空载欧洲网络服务器的平均响应时间；我们还需要了解该地区所有网络服务器的响应时间分布。这些知识使我们能够识别导致尾部延迟的因素。

At the scale our systems operate, being alerted for single-machine failures is unacceptable because such data is too noisy to be actionable. Instead we try to build systems that are robust against failures in the systems they depend on. Rather than requiring management of many individual components, a large system should be designed to aggregate signals and prune outliers. We need monitoring systems that allow us to alert for high-level service objectives, but retain the granularity to inspect individual components as needed.

在我们系统运行的规模上，收到单机故障警报是不可接受的，因为此类数据噪音太大，无法采取行动。相反，我们尝试构建能够抵抗它们所依赖的系统中的故障的系统。与其要求管理许多单独的组件，不如设计一个大型系统来聚合信号和筛选异常值。我们需要监控系统，使我们能够针对高级服务目标发出警报，但保留粒度以根据需要检查各个组件。

Google’s monitoring systems evolved over the course of 10 years from the traditional model of custom scripts that check responses and alert, wholly separated from visual display of trends, to a new paradigm. This new model made the collection of time-series a first-class role of the monitoring system, and replaced those check scripts with a rich language for manipulating time-series into charts and alerts.

在10年的时间里，Google的监控系统从传统的检查响应和警报的自定义脚本模型演变为一个新的模型。这种新模型使时间序列的收集成为监控系统的主要角色，并用丰富的语言取代了那些检查脚本，用于将时间序列转换为成图表和警报。

* [The Rise of Borgmon（Borgmon的兴起）](the_rise_of_borgmon.md)
* [Instrumentation of Applications（应用程序检测）](instrumentation_of_applications.md)
* [](collection_of_exported_data.md)
* [](storage_in_the_time-series_arena.md)
* [](rule_evaluation.md)
* [](alerting.md)
* [](sharding_the_monitoring_topology.md)
* [](black-box_monitoring.md)
* [](maintaining_the_configuration.md)
* [](ten_years_on.md)
