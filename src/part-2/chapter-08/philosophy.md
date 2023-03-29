## **Philosophy**

## **理念**

Release engineering is guided by an engineering and service philosophy that’s expressed through four major principles, detailed in the following sections.

发布工程以工程和服务理念为指导，该理念通过四项主要原则表达，在以下各节中详述。

<br>

### **Self-Service Model**

### **自助服务模式**

In order to work at scale, teams must be self-sufficient. Release engineering has developed best practices and tools that allow our product development teams to control and run their own release processes. Although we have thousands of engineers and products, we can achieve a high release velocity because individual teams can decide how often and when to release new versions of their products. Release processes can be automated to the point that they require minimal involvement by the engineers, and many projects are automatically built and released using a combination of our automated build system and our deployment tools. Releases are truly automatic, and only require engineer involvement if and when problems arise.

为了大规模工作，团队必须自给自足。发布工程开发了最佳实践和工具，使我们的产品开发团队能够控制和运行他们自己的发布流程。尽管我们有成千上万的工程师和产品，但我们可以实现高发布速度，因为各个团队可以决定发布产品新版本的频率和时间。发布过程可以自动化到不需要工程师参与的程度，并且许多项目是使用我们的自动构建系统和部署工具的组合自动构建和发布的。发布是真正自动的，只有在出现问题时才需要工程师参与。

<br>

### **High Velocity**

### **高速**

User-facing software (such as many components of Google Search) is rebuilt frequently, as we aim to roll out customer-facing features as quickly as possible. We have embraced the philosophy that frequent releases result in fewer changes between versions. This approach makes testing and troubleshooting easier. Some teams perform hourly builds and then select the version to actually deploy to production from the resulting pool of builds. Selection is based upon the test results and the features contained in a given build. Other teams have adopted a "Push on Green" release model and deploy every build that passes all tests [[Kle14]](https://www.usenix.org/publications/login/october-2014-vol-39-no-5/making-push-green-reality).

面向用户的软件（例如Google搜索的许多组件）经常重建，因为我们的目标是尽快推出面向客户的功能。我们已经接受了这样一种理念，即频繁发布会导致版本之间的更改更少。这种方法使测试和故障排除更加容易。一些团队每小时执行一次构建，然后从生成的构建池中选择要实际部署到生产中的版本。选择基于测试结果和给定构建中包含的功能。其他团队采用了“Push on Green”发布模型并部署通过所有测试的每个构建 [[Kle14]](https://www.usenix.org/publications/login/october-2014-vol-39-no-5/making-push-green-reality)。

<br>

### **Hermetic Builds**

### **封闭构建**

Build tools must allow us to ensure consistency and repeatability. If two people attempt to build the same product at the same revision number in the source code repository on different machines, we expect identical results. Our builds are hermetic, meaning that they are insensitive to the libraries and other software installed on the build machine. Instead, builds depend on known versions of build tools, such as compilers, and dependencies, such as libraries. The build process is self-contained and must not rely on services that are external to the build environment.

构建工具必须让我们能够确保一致性和可重复性。如果两个人试图在不同机器上的源代码存储库中以相同的版本号构建相同的产品，我们期望得到相同的结果。我们的构建是封闭的，这意味着它们对构建机器上安装的库和其他软件不敏感。相反，构建依赖于已知版本的构建工具（例如编译器）和依赖项（例如库）。构建过程是独立的，不能依赖构建环境外部的服务。

Rebuilding older releases when we need to fix a bug in software that’s running in production can be a challenge. We accomplish this task by rebuilding at the same revision as the original build and including specific changes that were submitted after that point in time. We call this tactic cherry picking. Our build tools are themselves versioned based on the revision in the source code repository for the project being built. Therefore, a project built last month won’t use this month’s version of the compiler if a cherry pick is required, because that version may contain incompatible or undesired features.

当我们需要修复生产中运行的软件中的错误时，重建旧版本可能是一个挑战。我们通过在与原始构建相同的修订版中重建并包括在该时间点之后提交的特定更改来完成此任务。我们称这种策略为樱桃采摘。我们的构建工具本身根据正在构建的项目的源代码存储库中的修订版本进行版本控制。因此，如果需要挑选，上个月构建的项目将不会使用本月版本的编译器，因为该版本可能包含不兼容或不需要的功能。

<br>

### **Enforcement of Policies and Procedures**

### **政策和程序的执行**

Several layers of security and access control determine who can perform specific operations when releasing a project. Gated operations include:

* Approving source code changes—this operation is managed through configuration files scattered throughout the codebase
* Specifying the actions to be performed during the release process
* Creating a new release
* Approving the initial integration proposal (which is a request to perform a build at a specific revision number in the source code repository) and subsequent cherry picks
* Deploying a new release
* Making changes to a project’s build configuration

安全和访问控制决定了谁可以在发布项目时执行特定操作。风控操作包括：

* 批准源代码更改——此操作通过分散在代码库中的配置文件进行管理
* 指定发布过程中要执行的动作
* 创建一个新版本
* 批准初始集成提案（这是在源代码存储库中以特定修订号执行构建的请求）和后续的挑选
* 部署新版本
* 更改项目的构建配置

Almost all changes to the codebase require a code review, which is a streamlined action integrated into our normal developer workflow. Our automated release system produces a report of all changes contained in a release, which is archived with other build artifacts. By allowing SREs to understand what changes are included in a new release of a project, this report can expedite troubleshooting when there are problems with a release.

几乎所有对代码库的更改都需要代码审查，这是集成到我们正常开发人员工作流程中的简化操作。我们的自动发布系统生成一份包含在发布中的所有更改的报告，该报告与其他构建日志一起存档。通过让SRE了解项目的新版本中包含哪些更改，此报告可以在版本出现问题时加快故障排除。

<br>

---

**[Back to contents of the chapter（返回章节目录）](release_engineering.md)**

* **Previous Section（上一节）：[The Role of a Release Engineer（发布工程师的角色）](the_role_of_a_release_engineer.md)**
* **Next Section（下一节）：[Continuous Build and Deployment（持续集成和部署）](continuous_build_and_deployment.md)**
