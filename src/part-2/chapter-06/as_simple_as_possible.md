## **As Simple as Possible, No Simpler**

## **尽可能的简单**

Piling all these requirements on top of each other can add up to a very complex monitoring system—your system might end up with the following levels of complexity:

* Alerts on different latency thresholds, at different percentiles, on all kinds of different metrics
* Extra code to detect and expose possible causes
* Associated dashboards for each of these possible causes

将所有这些要求堆积在一起，就会形成一个非常复杂的监控系统--你的系统最终可能具有以下复杂程度：

* 在不同的延迟阈值、不同的百分位数、各种不同的指标上发出警报
* 额外的代码来检测和暴露可能的原因
* 为每个可能的原因提供相关的仪表板

The sources of potential complexity are never-ending. Like all software systems, monitoring can become so complex that it’s fragile, complicated to change, and a maintenance burden.

潜在的复杂性的来源是永无止境的。像所有的软件系统一样，监控可能变得如此复杂，以至于它很脆弱，改变起来很复杂，而且是一个维护负担。

Therefore, design your monitoring system with an eye toward simplicity. In choosing what to monitor, keep the following guidelines in mind:

* The rules that catch real incidents most often should be as simple, predictable, and reliable as possible.
* Data collection, aggregation, and alerting configuration that is rarely exercised (e.g., less than once a quarter for some SRE teams) should be up for removal.
* Signals that are collected, but not exposed in any prebaked dashboard nor used by any alert, are candidates for removal.

因此，在设计你的监控系统时，要着眼于简单。在选择监控内容时，请牢记以下准则：

* 最经常捕捉到真实事件的规则应该是尽可能简单、可预测和可靠的。
* 很少使用的数据收集、汇总和警报配置（例如，对于一些SRE团队来说，不到一个季度一次）应该被删除。
* 收集到的信号，但没有暴露在任何仪表盘中，也没有被任何警报器使用，是可以被删除的候选信号。

In Google’s experience, basic collection and aggregation of metrics, paired with alerting and dashboards, has worked well as a relatively standalone system. (In fact Google’s monitoring system is broken up into several binaries, but typically people learn about all aspects of these binaries.) It can be tempting to combine monitoring with other aspects of inspecting complex systems, such as detailed system profiling, single- process debugging, tracking details about exceptions or crashes, load testing, log collection and analysis, or traffic inspection. While most of these subjects share commonalities with basic monitoring, blending together too many results in overly complex and fragile systems. As in many other aspects of software engineering, maintaining distinct systems with clear, simple, loosely coupled points of integration is a better strategy (for example, using web APIs for pulling summary data in a format that can remain constant over an extended period of time).

根据谷歌的经验，基本的指标收集和汇总，再配上警报和仪表盘，作为一个相对独立的系统，效果不错。（事实上，谷歌的监控系统被分解成几个部分，但通常人们会了解这些部分的所有方面）。将监控与检查复杂系统的其他方面结合起来可能是很诱人的，比如详细的系统剖析、单一的进程调试、跟踪异常或崩溃的细节、负载测试、日志收集和分析或流量检查。虽然这些主题中的大多数与基本监控有共同之处，但将太多的主题混合在一起会导致系统过于复杂和脆弱。就像软件工程的许多其他方面一样，维护具有明确、简单、松散耦合的集成点的不同系统是一个更好的策略（例如，使用Web APIs来拉取摘要数据，其格式可以在很长一段时间内保持不变）。
