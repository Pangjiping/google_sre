## **System Stability Versus Agility**

## **系统稳定性与敏捷性**

It sometimes makes sense to sacrifice stability for the sake of agility. I’ve often approached an unfamiliar problem domain by conducting what I call exploratory coding—setting an explicit shelf life for whatever code I write with the understanding that I’ll need to try and fail once in order to really understand the task I need to accomplish. Code that comes with an expiration date can be much more liberal with test coverage and release management because it will never be shipped to production or be seen by users.

有时为了敏捷而牺牲稳定性是有意义的。我经常通过进行我称之为探索性编码的方式来处理一个不熟悉的问题——为我编写的任何代码设置一个明确的保质期，并理解我需要尝试并失败一次才能真正理解我需要完成的任务。带有到期时间的代码在测试范围和发布管理方面可以更加自由，因为它永远不会被运送到生产环境或被用户看到。

For the majority of production software systems, we want a balanced mix of stability and agility. SREs work to create procedures, practices, and tools that render software more reliable. At the same time, SREs ensure that this work has as little impact on developer agility as possible. In fact, SRE’s experience has found that reliable processes tend to actually increase developer agility: rapid, reliable production rollouts make changes in production easier to see. As a result, once a bug surfaces, it takes less time to find and fix that bug. Building reliability into development allows developers to focus their attention on what we really do care about—the functionality and performance of their software and systems.

对于大多数生产软件系统，我们需要稳定性和敏捷性的平衡组合。SRE致力于创建使软件更可靠的程序、实践和工具。同时，SRE确保这项工作对开发人员的敏捷性影响尽可能小。事实上，SRE的经验发现，可靠的流程实际上往往会提高开发人员的敏捷性：快速、可靠的发布使生产中的变化更容易被看到。因此，一旦出现错误，查找和修复该错误所需的时间就会减少。在开发中建立可靠性可以让开发人员将注意力集中在我们真正关心的事情上——他们的软件和系统的功能和性能。
