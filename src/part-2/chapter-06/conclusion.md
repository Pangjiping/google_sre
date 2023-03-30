## **Conclusion**

## **总结**

A healthy monitoring and alerting pipeline is simple and easy to reason about. It focuses primarily on symptoms for paging, reserving cause-oriented heuristics to serve as aids to debugging problems. Monitoring symptoms is easier the further "up" your stack you monitor, though monitoring saturation and performance of subsystems such as databases often must be performed directly on the subsystem itself. Email alerts are of very limited value and tend to easily become overrun with noise; instead, you should favor a dashboard that monitors all ongoing subcritical problems for the sort of information that typically ends up in email alerts. A dashboard might also be paired with a log, in order to analyze historical correlations.

一个健康的监控和警报流水线是简单和容易推理的。它主要集中在呼叫的问题上，保留面向原因的启发式方法来作为调试问题的辅助手段。监控问题是很容易的，你监控的堆栈越往上走，虽然监控饱和度和数据库等子系统的性能，往往必须直接在子系统本身上执行。电子邮件警报的价值非常有限，而且很容易被噪音淹没；相反，你应该支持一个仪表板，监控所有正在进行的次关键问题，以获得通常在电子邮件警报中出现的那种信息。仪表板也可以与日志配对，以分析历史上的关联性。

Over the long haul, achieving a successful on-call rotation and product includes choosing to alert on symptoms or imminent real problems, adapting your targets to goals that are actually achievable, and making sure that your monitoring supports rapid diagnosis.

从长远来看，实现成功的待命轮换和产品包括选择对症状或即将发生的实际问题发出警报，将你的目标调整为实际可以实现的目标，并确保你的监测支持快速诊断。

<br>

---

**[Back to contents of the chapter（返回章节目录）](monitoring_distributed_systems.md)**

* **Previous Section（上一节）：[Monitoring for the Long Term（长期监控）](monitoring_for_the_long_term.md)**
* **Next Chapter（下一章）：[The Evolution of Automation at Google（Google的自动化进程）](../chapter-07/the_evolution_of_automation_at_google.md)**
