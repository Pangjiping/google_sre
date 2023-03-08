# **Embracing Risk**

# **拥抱风险**

> Written by Marc Alvidrez
>
> Edited by Kavita Guliani

You might expect Google to try to build 100% reliable services—ones that never fail. It turns out that past a certain point, however, increasing reliability is worse for a service (and its users) rather than better! Extreme reliability comes at a cost: maximizing stability limits how fast new features can be developed and how quickly products can be delivered to users, and dramatically increases their cost, which in turn reduces the numbers of features a team can afford to offer. Further, users typically don’t notice the difference between high reliability and extreme reliability in a service, because the user experience is dominated by less reliable components like the cellular network or the device they are working with. Put simply, a user on a 99% reliable smartphone cannot tell the difference between 99.99% and 99.999% service reliability! With this in mind, rather than simply maximizing uptime, Site Reliability Engineering seeks to balance the risk of unavailability with the goals of rapid innovation and efficient service operations, so that users’ overall happiness—with features, service, and performance—is optimized.

你可能期望谷歌会尽力打造百分之百可靠的服务——即从不出现故障的服务。然而，事实证明，对于一个服务（以及其用户），过度追求可靠性会产生负面影响，而不是积极作用！极端的可靠性是有代价的：最大化稳定性会限制新功能的开发速度和产品交付给用户的速度，并且显著增加成本，这反过来又降低了团队可以提供的功能数量。此外，用户通常不会注意到服务的高可靠性和极端可靠性之间的差异，因为用户体验主要受到像蜂窝网络或他们正在使用的设备等可靠性较低的组件的影响。简单地说，使用99%可靠的智能手机的用户无法区分99.99%和99.999%的服务可靠性之间的差别！因此，SRE不仅仅是简单地最大化运行时间，而是在可用性不可避免存在的风险和快速创新以及高效的服务操作目标之间寻求平衡，以优化用户的整体幸福感——包括功能、服务和性能。

- [Managing Risk（管理风险）](managing_risk.md)
- [Measuring Service Risk（衡量服务风险）](measuring_service_risk.md)
- [Risk Tolerance of Services（服务的风险承受能力）](risk_tolerance_of_services.md)
- [Motivation for Error Budgets（错误预算的动机）](motivation_for_error_budgets.md)
