## **The Rise of Borgmon**

## **Borgmon的兴起**

Shortly after the job scheduling infrastructure Borg [[Ver15]](https://research.google.com/pubs/pub43438.html) was created in 2003, a new monitoring system—Borgmon—was built to complement it.

在2003年创建作业调度基础设施Borg[[Ver15]](https://research.google.com/pubs/pub43438.html)后不久，一个新的监控系统Borgmon被构建来对其进行补充。

Instead of executing custom scripts to detect system failures, Borgmon relies on a common data exposition format; this enables mass data collection with low overheads and avoids the costs of subprocess execution and network connection setup. We call this white-box monitoring (see [Chapter 6](../../part-2/chapter-06/black-box_versus_white-box.md) for a comparison of white-box and black-box monitoring).

Borgmon不是执行自定义脚本来检测系统故障，而是依赖于一种通用的数据展示格式；这能够以低开销收集大量数据，并避免子流程执行和网络连接设置的成本。我们称此为白盒监控（有关白盒和黑盒监控的比较，请参阅[第6章]((../../part-2/chapter-06/black-box_versus_white-box.md))）。

The data is used both for rendering charts and creating alerts, which are accomplished using simple arithmetic. Because collection is no longer in a short-lived process, the history of the collected data can be used for that alert computation as well.

这些数据用于呈现图表和创建警报，这些都是使用简单的算法完成的。因为收集不再是一个短暂的过程，所收集数据的历史也可以用于警报计算。

These features help to meet the goal of simplicity described in Chapter 6. They allow the system overhead to be kept low so that the people running the services can remain agile and respond to continuous change in the system as it grows.

这些特性有助于实现第6章中描述的简单性目标。它们允许将系统开销保持在较低水平，以便运行服务的人员可以保持敏捷并响应不断变化的系统。

To facilitate mass collection, the metrics format had to be standardized. An older method of exporting the internal state (known as `varz`) was formalized to allow the collection of all metrics from a single target in one HTTP fetch. For example, to view a page of metrics manually, you could use the following command:

为了完成大规模收集，度量格式必须标准化。一种导出内部状态的旧方法（称为`varz`）已正式化，以允许在一次HTTP请求中从单个目标收集所有指标。例如，要手动查看指标页面，您可以使用以下命令：

```bash
$ curl http://webserver:80/varz 
http_requests 37
errors_total 12
```

A Borgmon can collect from other Borgmon,3 so we can build hierarchies that follow the topology of the service, aggregating and summarizing information and discarding some strategically at each level. Typically, a team runs a single Borgmon per cluster, and a pair at the global level. Some very large services shard below the cluster level into many scraper Borgmon, which in turn feed to the cluster-level Borgmon.

一个Borgmon可以从其他Borgmon收集信息，因此我们可以构建遵循服务拓扑结构的层次结构，聚合和总结信息，并在每个级别战略性地丢弃一些信息。通常，一个团队在每个集群上运行一个Borgmon，并在全局级别运行一对。一些非常大的服务在集群级别以下分片成许多scraper Borgmon，这些Borgmon又提供给集群级别的Borgmon。
