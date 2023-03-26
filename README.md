# Site Reliability Engineering

Site Reliability Engineering: How Google Runs Production Systems中文译

更新中...

供自我学习使用，如果翻译有错误或者术语问题可以在issue和PR中讨论。

# **目录（Contents）**

* **[Foreword（前言）](./src/foreword.md)**
* **[Preface（序言）](./src/preface.md)**
* **[Part I. Introduction（介绍）](./src/part-1/introduction.md)**
  * [Chapter 1. Introduction（介绍）](./src/part-1/chapter-01/introduction.md)
    * [The Sysadmin Approach to Service Management（系统管理员的服务管理方法）](./src/part-1/chapter-01/the_sysadmin_approach_to_service_management.md)
    * [Google’s Approach to Service Management:Site Reliability Engineering（谷歌的服务管理方法：SRE）](./src/part-1/chapter-01/google's_approach_to_service_management_site_reliability_engineering.md)
    * [Tenets of SRE（SRE的原则）](./src/part-1/chapter-01/tenets_of_sre.md)
    * [The End of the Beginning（本章结语）](./src/part-1/chapter-01/the_end_of_the_beginning.md)
  * [Chapter 2. The Production Environment at Google, from the Viewpoint of an SRE（从SRE的角度介绍Google的生产环境）](./src/part-1/chapter-02/the_production_environment_at_google_from_the_viewpoint_of_an_sre.md)
    * [Hardware（硬件）](./src/part-1/chapter-02/hardware.md)
    * [System Software That “Organizes” the Hardware（“组织”硬件的系统软件）](./src/part-1/chapter-02/system_software_that_"organizes"_the_hardware.md)
    * [Other System Software（其他系统软件）](./src/part-1/chapter-02/other_system_software.md)
    * [Our Software Infrastructure（软件基础设施）](./src/part-1/chapter-02/our_software_infra.md)
    * [Our Development Environment（开发环境）](./src/part-1/chapter-02/our_development_env.md)
    * [Shakespeare: A Sample Service（Shakespeare：一个示例服务）](./src/part-1/chapter-02/shakespare_a_simple_service.md)
* **[Part II. Principles（原则）](./src/part-2/principles.md)**
  * [Chapter 3. Embracing Risk（拥抱风险）](./src/part-2/chapter-03/embracing_risk.md)
    * [Managing Risk（管理风险）](./src/part-2/chapter-03/managing_risk.md)
    * [Measuring Service Risk（衡量服务风险）](./src/part-2/chapter-03/measuring_service_risk.md)
    * [Risk Tolerance of Services（服务的风险承受能力）](./src/part-2/chapter-03/risk_tolerance_of_services.md)
    * [Motivation for Error Budgets（错误预算）](./src/part-2/chapter-03/motivation_for_error_budgets.md)
  * [Chapter 4. Service Level Objectives（服务水平目标）](./src/part-2/chapter-04/service_level_objectives.md)
    * [Service Level Terminology（服务水平术语）](./src/part-2/chapter-04/service_level_terminology.md)
    * [Indicators in Practice（实践中的SLI）](./src/part-2/chapter-04/indicators_in_practice.md)
    * [Objectives in Practice（实践中的SLO）](./src/part-2/chapter-04/objectives_in_practice.md)
    * [Agreements in Practice（实践中的SLA）](./src/part-2/chapter-04/agreements_in_practice.md)
  * [Chapter 5.Eliminating Toil（消除劳作）](./src/part-2/chapter-05/eliminating_toil.md)
    * [Toil Defined（劳作的定义）](./src/part-2/chapter-05/toil_defined.md)
    * [Why Less Toil Is Better（为什么更少的劳作更好）](./src/part-2/chapter-05/why_less_toil_is_better.md)
    * [What Qualifies as Engineering?（什么符合工程的标准）](./src/part-2/chapter-05/what_qualifies_as_engineering.md)
    * [Is Toil Always Bad?（劳作总是不好的吗？）](./src/part-2/chapter-05/is_toil_always_bad.md)
    * [Conclusion（总结）](./src/part-2/chapter-05/conclusion.md)
  * [Chapter 6.Monitoring Distributed Systems（监控分布式系统）](./src/part-2/chapter-06/monitoring_distributed_systems.md)
    * [Definitions（定义）](./src/part-2/chapter-06/definitions.md)
    * [Why Monitor?（为什么要监控）](./src/part-2/chapter-06/why_monitor.md)
    * [Setting Reasonable Expectations for Monitoring（设定合理的监控期望值）](./src/part-2/chapter-06/setting_reasonable_expectations_for_monitoring.md)
    * [Symptoms Versus Causes（症状与原因）](./src/part-2/chapter-06/symptoms_versus_causes.md)
    * [Black-Box Versus White-Box（黑盒与白盒）](./src/part-2/chapter-06/black-box_versus_white-box.md)
    * [The Four Golden Signals（四种黄金信号）](./src/part-2/chapter-06/the_four_golden_signals.md)
    * [Worrying About Your Tail (or, Instrumentation and Performance)（小心拖尾数据（或者，仪表和性能））](./src/part-2/chapter-06/worrying_about_your_tail.md)
    * [Choosing an Appropriate Resolution for Measurements（为测量选择一个合适的分辨率）](./src/part-2/chapter-06/choosing_an_appropriate_resolution_for_measurements.md)
    * [As Simple as Possible, No Simpler（尽可能地简单）](./src/part-2/chapter-06/as_simple_as_possible.md)
    * [Tying These Principles Together（将这些原则联系起来）](./src/part-2/chapter-06/tying_these_principles_together.md)
    * [Monitoring for the Long Term（长期监控）](./src/part-2/chapter-06/monitoring_for_the_long_term.md)
    * [Conclusion（总结）](./src/part-2/chapter-06/conclusion.md)
