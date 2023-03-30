## **Modularity**

## **模块化**

Expanding outward from APIs and single binaries, many of the rules of thumb that apply to object-oriented programming also apply to the design of distributed systems. The ability to make changes to parts of the system in isolation is essential to creating a supportable system. Specifically, loose coupling between binaries, or between binaries and configuration, is a simplicity pattern that simultaneously promotes developer agility and system stability. If a bug is discovered in one program that is a component of a larger system, that bug can be fixed and pushed to production independent of the rest of the system.

从API和单个二进制文件向外扩展，许多适用于面向对象编程的经验法则也适用于分布式系统的设计。独立地对系统的各个部分进行更改的能力对于创建可支持的系统至关重要。具体来说，**二进制文件之间或二进制文件与配置之间的松耦合是一种可同时提高开发人员敏捷性和系统稳定性的简单模式。如果在作为更大系统组件的一个程序中发现错误，则可以修复该错误并独立于系统的其余部分将其推送到生产环境。**

While the modularity that APIs offer may seem straightforward, it is not so apparent that the notion of modularity also extends to how changes to APIs are introduced. Just a single change to an API can force developers to rebuild their entire system and run the risk of introducing new bugs. Versioning APIs allows developers to continue to use the version that their system depends upon while they upgrade to a newer version in a safe and considered way. The release cadence can vary throughout a system, instead of requiring a full production push of the entire system every time a feature is added or improved.

虽然API提供的模块化可能看起来很简单，但模块化的概念也扩展到如何引入API的更改并不那么明显。仅对API进行一次更改就可能迫使开发人员重建他们的整个系统，并冒着引入新错误的风险。版本控制API允许开发人员继续使用其系统所依赖的版本，同时以安全且经过深思熟虑的方式升级到更新的版本。整个系统的发布节奏可能会有所不同，而不是每次添加或改进功能时都需要对整个系统进行全面的生产推送。

As a system grows more complex, the separation of responsibility between APIs and between binaries becomes increasingly important. This is a direct analogy to object- oriented class design: just as it is understood that it is poor practice to write a "grab bag" class that contains unrelated functions, it is also poor practice to create and put into production a "util" or "misc" binary. A well-designed distributed system consists of collaborators, each of which has a clear and well-scoped purpose.

随着系统变得越来越复杂，API之间和二进制文件之间的职责分离变得越来越重要。这是对面向对象类设计的直接类比：正如人们所理解的那样，编写包含不相关功能的“抓包”类是不好的做法，创建并投入生产“util”也是不好的做法。一个设计良好的分布式系统由协作者组成，每个协作者都有明确且范围明确的目的。

The concept of modularity also applies to data formats. One of the central strengths and design goals of Google’s protocol buffers3 was to create a wire format that was backward and forward compatible.

模块化的概念也适用于数据格式。Google protocol buffers的核心优势和设计目标之一是创建一种向后和向前兼容的格式。

<br>

---

**[Back to contents of the chapter（返回章节目录）](simplicity.md)**

* **Previous Section（上一节）：[Minimal APIs（最小化API）](minimal_apis.md)**
* **Next Section（下一节）：[Release Simplicity（发布简洁性）](release_simplicity.md)**
