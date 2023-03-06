## **Other System Software**

## **其他系统软件**

Several other components in a datacenter are also important.

数据中心中还有其他几个重要的组件。

<br>

### **Lock Service**

### **锁服务**

The Chubby [[Bur06]](https://research.google.com/archive/chubby.html) lock service provides a filesystem-like API for maintaining locks. Chubby handles these locks across datacenter locations. It uses the Paxos protocol for asynchronous Consensus (see Chapter 23).

Chubby [[Bur06]](https://research.google.com/archive/chubby.html) 是一种锁服务，提供类似文件系统的API来维护锁。Chubby可以处理来自不同数据中心不同位置的锁，它使用Paxos协议来实现异步共识（参见第23章）。

Chubby also plays an important role in master election. When a service has five replicas of a job running for reliability purposes but only one replica may perform actual work, Chubby is used to select which replica may proceed.

Chubby还在主节点选举中扮演着重要的角色。当一个服务运行了五个副本以保证可靠性，但只有一个副本可以执行实际工作时，使用Chubby来选择哪个副本可以继续工作。

Data that must be consistent is well suited to storage in Chubby. For this reason, BNS uses Chubby to store mapping between BNS paths and `IP address:port` pairs.

数据需要保持一致性的情况适合存储在Chubby中。因此，BNS使用Chubby来存储BNS路径和`IP address:port`对之间的映射关系。

<br>

### **Monitoring and Alerting**

### **监控和告警**

We want to make sure that all services are running as required. Therefore, we run many instances of our Borgmon monitoring program (see Chapter 10). Borgmon regularly “scrapes” metrics from monitored servers. These metrics can be used instantaneously for alerting and also stored for use in historic overviews (e.g., graphs). We can use monitoring in several ways:

* Set up alerting for acute problems.
* Compare behavior: did a software update make the server faster?
* Examine how resource consumption behavior evolves over time, which is essential for capacity planning.

我们希望确保所有服务都按照要求运行。因此，我们运行许多Borgmon监视程序实例（请参阅第10章）。Borgmon定期从受监视服务器“抓取”指标。这些指标可以立即用于警报，并存储供历史概览使用（例如，图表）。我们可以使用监视以多种方式：

* 短期问题设置警报。
* 比较行为：软件更新是否使服务器更快？
* 我们需要监测资源消耗的行为随时间的演变，这对于容量规划是至关重要的。

<br>

---

**[Back to contents of the chapter（返回章节目录）](the_production_environment_at_google_from_the_viewpoint_of_an_sre.md)**

* **Previous Section（上一节）：[System Software That “Organizes” the Hardware（“组织”硬件的系统软件）](system_software_that_%22organizes%22_the_hardware.md)**
* **Next Section（下一节）：[Our Software Infrastructure（软件基础设施）](our_software_infra.md)**
