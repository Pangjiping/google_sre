## **Choosing an Appropriate Resolution for Measurements**

## **为测量选择一个合适的分辨率**

Different aspects of a system should be measured with different levels of granularity. For example:

* Observing CPU load over the time span of a minute won’t reveal even quite long-lived spikes that drive high tail latencies.
* On the other hand, for a web service targeting no more than 9 hours aggregate downtime per year (99.9% annual uptime), probing for a 200 (success) status more than once or twice a minute is probably unnecessarily frequent.
* Similarly, checking hard drive fullness for a service targeting 99.9% availability more than once every 1–2 minutes is probably unnecessary.

一个系统的不同方面应以不同的颗粒度来衡量。比如说：

* 在一分钟的时间跨度内观察CPU负载，甚至不会发现高尾部延迟。
* 对于一个目标是每年累计停机时间不超过9小时（年正常运行时间为99.9%）的网络服务来说，每分钟探测200（成功）状态一次或两次以上可能是不必要的。
* 同样，对于一个以99.9%的可用性为目标的服务来说，每1-2分钟检查一次以上的硬盘饱和度可能是不必要的。

Take care in how you structure the granularity of your measurements. Collecting per-second measurements of CPU load might yield interesting data, but such frequent measurements may be very expensive to collect, store, and analyze. If your monitoring goal calls for high resolution but doesn’t require extremely low latency, you can reduce these costs by performing internal sampling on the server, then configuring an external system to collect and aggregate that distribution over time or across servers. You might:

1. Record the current CPU utilization each second.
2. Using buckets of 5% granularity, increment the appropriate CPU utilization bucket each second.
3. Aggregate those values every minute.

注意你如何构建你的测量的粒度。收集每秒钟的CPU负载测量值可能会产生有趣的数据，但是这种频繁的测量值在收集、存储和分析时可能会非常昂贵。如果你的监控目标要求高分辨率，但不需要极低的延迟，你可以通过在服务器上执行内部采样来减少这些成本，然后配置一个外部系统来收集和汇总随时间或跨服务器的分布。你可以：

1. 每秒钟记录当前的CPU利用率。
2. 使用5%粒度的桶，每秒钟递增适当的CPU利用率桶。
3. 每分钟对这些数值进行汇总。

This strategy allows you to observe brief CPU hotspots without incurring very high cost due to collection and retention.

这种策略允许你观察短暂的CPU热点，而不会因为收集和保留而产生非常高的成本。
