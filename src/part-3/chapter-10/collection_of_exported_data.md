## **Collection of Exported Data**

## **收集导出的数据**

To find its targets, a Borgmon instance is configured with a list of targets using one of many name resolution methods. The target list is often dynamic, so using service discovery reduces the cost of maintaining it and allows the monitoring to scale.

为了找到它的目标，Borgmon实例使用许多名称解析方法配置了一个目标列表。目标列表通常是动态的，因此使用服务发现可以降低维护它的成本并允许扩展监控。

At predefined intervals, Borgmon fetches the `/varz` URI on each target, decodes the results, and stores the values in memory. Borgmon also spreads the collection from each instance in the target list over the whole interval, so that collection from each target is not in lockstep with its peers.

在预定义的时间间隔内，Borgmon获取每个目标上的`/varz`URI，解码结果，并将值存储在内存中。Borgmon还将目标列表中每个实例的集合分布在整个时间间隔内，这样每个目标的集合就不会与其他实例重叠。

Borgmon also records "synthetic" variables for each target in order to identify:

* If the name was resolved to a host and port
* If the target responded to a collection
* If the target responded to a health check
* What time the collection finished

Borgmon 还记录了每个目标的“合成”变量，以便识别：

* 如果名称被解析为主机和端口
* 如果目标响应了一个集合
* 如果目标响应健康检查
* 收集完成的时间

These synthetic variables make it easy to write rules to detect if the monitored tasks are unavailable.

这些合成变量使编写规则以检测受监视任务是否可用变得容易。

It’s interesting that `varz` is quite dissimilar to SNMP (Simple Networking Monitoring Protocol), which "is designed [...] to have minimal transport requirements and to continue working when most other network applications fail" [[Mic03]](https://technet.microsoft.com/en-us/library/cc776379%28v=ws.10%29.aspx). Scraping targets over HTTP seems to be at odds with this design principle; however, experience shows that this is rarely an issue. The system itself is already designed to be robust against network and machine failures, and Borgmon allows engineers to write smarter alerting rules by using the collection failure itself as a signal.

有趣的是，`varz`与SNMP非常不同，SNMP“被设计为具有最小的传输要求并在大多数其他网络应用程序失败时继续工作”[[Mic03]](https://technet.microsoft.com/en-us/library/cc776379%28v=ws.10%29.aspx)。通过HTTP获取目标似乎与这个设计原则不一致；然而，经验表明这很少成为问题。系统本身已经被设计为能够抵抗网络和机器故障，Borgmon允许工程师通过使用收集故障本身作为信号来编写更智能的警报规则。
