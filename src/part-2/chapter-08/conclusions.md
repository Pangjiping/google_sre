## **Conclusions**

## **总结**

While this chapter has specifically discussed Google’s approach to release engineering and the ways in which release engineers work and collaborate with SREs, these practices can also be applied more widely.

虽然本章专门讨论了Google的发布工程方法以及发布工程师与SRE合作的方式，但这些实践也可以得到更广泛的应用。

<br>

### **It’s Not Just for Googlers**

### **不仅仅适用于Google工程师**

When equipped with the right tools, proper automation, and well-defined policies, developers and SREs shouldn’t have to worry about releasing software. Releases can be as painless as simply pressing a button.

当配备了正确的工具、适当的自动化和明确定义的策略时，开发人员和SRE应该不必担心发布软件。发布可以像简单地按下一个按钮一样轻松。

Most companies deal with the same set of release engineering problems regardless of their size or the tools they use: How should you handle versioning of your packages? Should you use a continuous build and deploy model, or perform periodic builds? How often should you release? What configuration management policies should you use? What release metrics are of interest?

大多数公司处理同一组发布工程问题，无论它们的规模或使用的工具如何：您应该如何处理包的版本控制？您应该使用持续构建和部署模型，还是执行定期构建？你应该多久发布一次？您应该使用哪些配置管理策略？哪些发布指标值得关注？

Google Release Engineers have developed our own tools out of necessity because open sourced or vendor-supplied tools don’t work at the scale we require. Custom tools allow us to include functionality to support (and even enforce) release process policies. However, these policies must first be defined in order to add appropriate features to our tools, and all companies should take the effort to define their release processes whether or not the processes can be automated and/or enforced.

出于需要，Google发布工程师开发了我们自己的工具，因为开源或供应商提供的工具无法在我们需要的规模下工作。自定义工具使我们能够包含支持发布流程策略的功能。但是，必须首先定义这些策略，以便为我们的工具添加适当的功能，并且所有公司都应该努力定义他们的发布流程，无论这些流程是否可以自动化或强制执行。

<br>

### **Start Release Engineering at the Beginning**

### **在项目开启时就开始发布工程**

Release engineering has often been an afterthought, and this way of thinking must change as platforms and services continue to grow in size and complexity.

发布工程通常是事后才想到的，随着平台和服务的规模和复杂性不断增长，这种思维方式必须改变。

Teams should budget for release engineering resources at the beginning of the product development cycle. It’s cheaper to put good practices and process in place early, rather than have to retrofit your system later.

团队应该在产品开发周期开始时为发布工程资源制定预算。尽早实施良好的实践和流程比晚些时候改造您的系统成本更低。

It is essential that the developers, SREs, and release engineers work together. The release engineer needs to understand the intention of how the code should be built and deployed. The developers shouldn’t build and "throw the results over the fence" to be handled by the release engineers.

开发人员、SRE和发布工程师一起工作至关重要。发布工程师需要了解应该如何构建和部署代码的意图。开发人员不应该构建并“将结果扔过篱笆”由发布工程师处理。

Individual project teams decide when release engineering becomes involved in a project. Because release engineering is still a relatively young discipline, managers don’t always plan and budget for release engineering in the early stages of a project. Therefore, when considering how to incorporate release engineering practices, be sure that you consider its role as applied to the entire lifecycle of your product or service—particularly the early stages.

各个项目团队决定发布工程何时参与项目。因为发布工程仍然是一门相对年轻的学科，所以管理人员并不总是在项目的早期阶段为发布工程制定计划和预算。因此，在考虑如何整合发布工程实践时，请务必考虑其作用应用于产品或服务的整个生命周期——尤其是早期阶段。

<br>

> More Information
>
> For more information on release engineering, see the following presentations, each of which has video available online:
>
> * [How Embracing Continuous Release Reduced Change Complexity](https://www.usenix.org/conference/ures14west/summit-program/presentation/dickson), USENIX Release Engineering Summit West 2014, [[Dic14]](http://usenix.org/conference/ures14west/summit-program/presentation/dickson)
> * [Maintaining Consistency in a Massively Parallel Environment](https://www.usenix.org/conference/ucms13/summit-program/presentation/mcnutt), USENIX Configuration Management Summit 2013, [[McN13]](https://www.usenix.org/conference/ucms13/summit-program/presentation/mcnutt)
> * [The 10 Commandments of Release Engineering](https://www.youtube.com/watch?v=RNMjYV_UsQ8), 2nd International Workshop on Release Engineering 2014, [[McN14b]](https://www.youtube.com/watch?v=RNMjYV_UsQ8)
> * [Distributing Software in a Massively Parallel Environment](https://www.usenix.org/conference/lisa14/conference-program/presentation/mcnutt), LISA 2014, [[McN14c]](https://www.usenix.org/conference/lisa14/conference-program/presentation/mcnutt)

<br>

---

**[Back to contents of the chapter（返回章节目录）](release_engineering.md)**

* **Previous Section（上一节）：[Continuous Build and Deployment（持续集成和部署）](continuous_build_and_deployment.md)**
* **Next Section（下一节）：[Conclusions（总结）](conclusions.md)**
