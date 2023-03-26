## **Worrying About Your Tail (or, Instrumentation and Performance)**

## **小心拖尾数据（或者，仪表和性能）**

When building a monitoring system from scratch, it’s tempting to design a system based upon the mean of some quantity: the mean latency, the mean CPU usage of your nodes, or the mean fullness of your databases. The danger presented by the latter two cases is obvious: CPUs and databases can easily be utilized in a very imbalanced way. The same holds for latency. If you run a web service with an average latency of 100 ms at 1,000 requests per second, 1% of requests might easily take 5 seconds.2 If your users depend on several such web services to render their page, the 99th percentile of one backend can easily become the median response of your frontend.

当从头开始建立一个监控系统时，很容易根据一些数量的平均值来设计一个系统：平均延迟，节点的平均CPU使用率，或者数据库的平均饱和度。后两种情况带来的危险是显而易见的：CPU和数据库很容易以一种非常不平衡的方式被利用。延迟也是如此。如果你运行一个平均延迟为100毫秒的网络服务，每秒有1000个请求，1%的请求可能很容易需要5秒钟。

The simplest way to differentiate between a slow average and a very slow "tail" of requests is to collect request counts bucketed by latencies (suitable for rendering a histogram), rather than actual latencies: how many requests did I serve that took between 0 ms and 10 ms, between 10 ms and 30 ms, between 30 ms and 100 ms, between 100 ms and 300 ms, and so on? Distributing the histogram boundaries approximately exponentially (in this case by factors of roughly 3) is often an easy way to visualize the distribution of your requests.

区分一个缓慢的平均请求和一个非常缓慢的“拖尾”的最简单方法是收集按延迟分类的请求数（适合渲染直方图），而不是实际的延迟：我提供的请求中有多少是在0毫秒到10毫秒之间，10毫秒到30毫秒之间，30毫秒到100毫秒之间，100毫秒到300毫秒之间，等等。将直方图的边界以近似指数的方式分布（在这种情况下，以大约3的系数分布），通常是可视化你的请求分布的一个简单方法。

<br>

---

**[Back to contents of the chapter（返回章节目录）](monitoring_distributed_systems.md)**

* **Previous Section（上一节）：[The Four Golden Signals（四种黄金信号）](the_four_golden_signals.md)**
* **Next Section（下一节）：[Choosing an Appropriate Resolution for Measurements（为测量选择一个合适的分辨率）](choosing_an_appropriate_resolution_for_measurements.md)**
