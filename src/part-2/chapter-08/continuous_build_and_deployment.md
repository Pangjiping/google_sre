## **Continuous Build and Deployment**

## **持续构建和部署**

Google has developed an automated release system called Rapid. Rapid is a system that leverages a number of Google technologies to provide a framework that delivers scalable, hermetic, and reliable releases. The following sections describe the software lifecycle at Google and how it is managed using Rapid and other associated tools.

Google开发了一个名为Rapid的自动发布系统。Rapid是一个利用多项Google技术提供框架的系统，该框架可提供可扩展、封闭且可靠的版本。以下部分介绍了Google的软件生命周期以及如何使用Rapid和其他相关工具对其进行管理。

<br>

### **Building**

### **构建**

Blaze is Google’s build tool of choice. It supports building binaries from a range of languages, including our standard languages of C++, Java, Python, Go, and JavaScript. Engineers use Blaze to define build targets (e.g., the output of a build, such as a JAR file), and to specify the dependencies for each target. When performing a build, Blaze automatically builds the dependency targets.

Blaze是Google的首选构建工具。它支持从多种语言构建二进制文件，包括我们的标准语言C++、Java、Python、Go和JavaScript。工程师使用Blaze来定义构建目标（例如，构建的输出，如JAR文件），并指定每个目标的依赖项。执行构建时，Blaze会自动构建依赖目标。

Build targets for binaries and unit tests are defined in Rapid’s project configuration files. Project-specific flags, such as a unique build identifier, are passed by Rapid to Blaze. All binaries support a flag that displays the build date, the revision number, and the build identifier, which allow us to easily associate a binary to a record of how it was built.

二进制文件和单元测试的构建目标在Rapid的项目配置文件中定义。特定于项目的标志，例如唯一的构建标识符，由Rapid传递给Blaze。所有二进制文件都支持显示构建日期、修订号和构建标识符的标志，这使我们可以轻松地将二进制文件与其构建方式的记录相关联。

<br>

### **Branching**

### **分支**

All code is checked into the main branch of the source code tree (mainline). However, most major projects don’t release directly from the mainline. Instead, we branch from the mainline at a specific revision and never merge changes from the branch back into the mainline. Bug fixes are submitted to the mainline and then cherry picked into the branch for inclusion in the release. This practice avoids inadvertently picking up unrelated changes submitted to the mainline since the original build occurred. Using this branch and cherry pick method, we know the exact contents of each release.

所有代码都被转入源代码的主分支（主线）。然而，大多数主要项目并不直接从主分支发布。相反，我们在特定修订版从主分支分支，并且永远不会将分支中的更改合并回主分支。错误修复被提交到主分支，然后被挑选到分支中以包含在发布中。这种做法可以避免无意中拾取自原始构建发生以来提交到主线的不相关更改。使用这种分支和cherry pick方法，我们知道每个版本的确切内容。

<br>

### **Testing**

### **测试**

A continuous test system runs unit tests against the code in the mainline each time a change is submitted, allowing us to detect build and test failures quickly. Release engineering recommends that the continuous build test targets correspond to the same test targets that gate the project release. We also recommend creating releases at the revision number (version) of the last continuous test build that successfully completed all tests. These measures decrease the chance that subsequent changes made to the mainline will cause failures during the build performed at release time.

每次提交更改时，持续测试系统都会针对主线中的代码运行单元测试，使我们能够快速检测构建和测试失败。发布工程建议持续构建测试目标对应于控制项目发布的相同测试目标。我们还建议在成功完成所有测试的最后一个连续测试版本的修订号（版本）上创建版本。这些措施减少了在发布时执行的构建期间对主线所做的后续更改导致失败的可能性。

During the release process, we re-run the unit tests using the release branch and create an audit trail showing that all the tests passed. This step is important because if a release involves cherry picks, the release branch may contain a version of the code that doesn’t exist anywhere on the mainline. We want to guarantee that the tests pass in the context of what’s actually being released.

在发布过程中，我们使用发布分支重新运行单元测试，并创建一个审计跟踪，显示所有测试都已通过。这一步很重要，因为如果发布涉及精选，发布分支可能包含主线上任何地方都不存在的代码版本。我们想保证测试在实际发布的环境中通过。

To complement the continuous test system, we use an independent testing environment that runs system-level tests on packaged build artifacts. These tests can be launched manually or from Rapid.

为了补充连续测试系统，我们使用一个独立的测试环境，对打包的构建组件运行系统级测试。这些测试可以手动启动或从Rapid启动。

<br>

### **Packaging**

### **打包**

Software is distributed to our production machines via the Midas Package Manager (MPM) [[McN14c]](https://www.usenix.org/conference/lisa14/conference-program/presentation/mcnutt). MPM assembles packages based on Blaze rules that list the build artifacts to include, along with their owners and permissions. Packages are named (e.g., search/shakespeare/frontend), versioned with a unique hash, and signed to ensure authenticity. MPM supports applying labels to a particular version of a package. Rapid applies a label containing the build ID, which guarantees that a package can be uniquely referenced using the name of the package and this label.

软件通过Midas包管理器（MPM）[[McN14c]](https://www.usenix.org/conference/lisa14/conference-program/presentation/mcnutt)分发到我们的生产机器。MPM根据列出要包含的构建组件及其所有者和权限的Blaze规则组装包。包被命名（例如search/shakespeare/frontend），使用唯一的散列进行版本控制，并签名以确保真实性。MPM支持将标签应用于特定版本的包。Rapid应用包含构建ID的标签，这保证可以使用包的名称和此标签来唯一引用包。

Labels can be applied to an MPM package to indicate a package’s location in the release process (e.g., dev, canary, or production). If you apply an existing label to a new package, the label is automatically moved from the old package to the new package. For example: if a package is labeled as canary, someone subsequently installing the canary version of that package will automatically receive the newest version of the package with the label canary.

标签可以应用于MPM包以指示包在发布过程中的位置（例如dev、canary或production）。如果将现有标签应用于新包，标签会自动从旧包移动到新包。例如：如果一个包被标记为canary，那么随后安装该包的canary版本的人将自动收到带有canary标签的最新版本的包。

<br>

### **Rapid**

### **Rapid**

Figure 8-1 shows the main components of the Rapid system. Rapid is configured with files called blueprints. Blueprints are written in an internal configuration language and are used to define build and test targets, rules for deployment, and administrative information (like project owners). Role-based access control lists determine who can perform specific actions on a Rapid project.

Figure 8-1展示了Rapid系统的主要组件。Rapid被称为蓝图的文件配置。蓝图是用内部配置语言编写的，用于定义构建和测试目标、部署规则和管理信息（如项目所有者）。基于角色的访问控制列表确定谁可以对Rapid项目执行特定操作。

![Simplified view of Rapid architecture showing the main components of the system](./figures/8-1.png)
> Figure 8-1. Simplified view of Rapid architecture showing the main components of the system

Each Rapid project has workflows that define the actions to perform during the release process. Workflow actions can be performed serially or in parallel, and a workflow can launch other workflows. Rapid dispatches work requests to tasks running as a Borg job on our production servers. Because Rapid uses our production infrastructure, it can handle thousands of release requests simultaneously.

每个Rapid项目都有定义发布过程中要执行的操作的工作流。工作流操作可以串行或并行执行，一个工作流可以启动其他工作流。Rapid将请求分派给在我们的生产服务器上作为Borg作业运行的任务。由于Rapid使用我们的生产基础设施，它可以同时处理数以千计的发布请求。

A typical release process proceeds as follows:

1. Rapid uses the requested integration revision number (often obtained automatically from our continuous test system) to create a release branch.
2. Rapid uses Blaze to compile all the binaries and execute the unit tests, often performing these two steps in parallel. Compilation and testing occur in environments dedicated to those specific tasks, as opposed to taking place in the Borg job where the Rapid workflow is executing. This separation allows us to parallelize work easily.
3. Build artifacts are then available for system testing and canary deployments. A typical canary deployment involves starting a few jobs in our production environment after the completion of system tests.
4. The results of each step of the process are logged. A report of all changes since the last release is created.

一个典型的发布过程如下所示：

1. Rapid使用请求的集成修订号（通常从我们的连续测试系统自动获取）来创建发布分支。
2. Rapid使用Blaze编译所有二进制文件并执行单元测试，通常并行执行这两个步骤。编译和测试发生在专用于这些特定任务的环境中，而不是发生在执行Rapid工作流的Borg作业中。这种分离使我们能够轻松地并行化工作。
3. 然后构建组件可用于系统测试和金丝雀部署。典型的金丝雀部署在完成系统测试后在我们的生产环境中启动一些作业。
4. 过程的每个步骤的结果都被记录下来。创建自上次发布以来所有更改的报告。

Rapid allows us to manage our release branches and cherry picks; individual cherry pick requests can be approved or rejected for inclusion in a release.

Rapid允许我们管理我们的发布分支和cherry-picks，可以批准或拒绝将个别cherry-pick请求包含在发布中。

<br>

### **Deployment**

### **部署**

Rapid is often used to drive simple deployments directly. It updates the Borg jobs to use newly built MPM packages based on deployment definitions in the blueprint files and specialized task executors.

Rapid通常用于直接驱动简单部署。它根据蓝图文件和专门的任务执行器中的部署定义更新Borg作业以使用新构建的MPM包。

For more complicated deployments, we use Sisyphus, which is a general-purpose rollout automation framework developed by SRE. A rollout is a logical unit of work that is composed of one or more individual tasks. Sisyphus provides a set of Python classes that can be extended to support any deployment process. It has a dashboard that allows for finer control on how the rollout is performed and provides a way to monitor the rollout’s progress.

对于更复杂的部署，我们使用Sisyphus，它是SRE开发的通用部署自动化框架。rollout是一个逻辑工作单元，由一个或多个单独的任务组成。Sisyphus提供了一组可以扩展以支持任何部署过程的Python类。它有一个仪表板，可以更好地控制rollout的执行方式，并提供一种方法来监控其进度。

In a typical integration, Rapid creates a rollout in a long-running Sisyphus job. Rapid knows the build label associated with the MPM package it created, and can specify that build label when creating the rollout in Sisyphus. Sisyphus uses the build label to specify which version of the MPM packages should be deployed.

在典型的集成中，Rapid在长期运行的Sisyphus作业中创建一个rollout。Rapid知道与其创建的MPM包关联的构建标签，并且可以在Sisyphus中创建rollout时指定该构建标签。Sisyphus使用构建标签来指定应该部署哪个版本的MPM包。

With Sisyphus, the rollout process can be as simple or complicated as necessary. For example, it can update all the associated jobs immediately or it can roll out a new binary to successive clusters over a period of several hours.

使用Sisyphus，推出过程可以根据需求简单或复杂。例如，它可以立即更新所有关联的作业，或者它可以在几个小时内将新的二进制文件推送到连续的集群。

Our goal is to fit the deployment process to the risk profile of a given service. In development or pre-production environments, we may build hourly and push releases automatically when all tests pass. For large user-facing services, we may push by starting in one cluster and expand exponentially until all clusters are updated. For sensitive pieces of infrastructure, we may extend the rollout over several days, interleaving them across instances in different geographic regions.

我们的目标是使部署过程适应给定服务的风险状况。在开发或预生产环境中，我们可能每小时构建一次，并在所有测试通过后自动推送发布。对于面向用户的大型服务，我们可能会从一个集群开始进行推送，然后呈指数级扩展，直到所有集群都更新完毕。对于基础设施的敏感部分，我们可能会将推送时间延长几天，将它们交错在不同地理区域的实例中。

<br>

---

**[Back to contents of the chapter（返回章节目录）](release_engineering.md)**

* **Previous Section（上一节）：[Configuration Management（配置管理）](configuration_management.md)**
* **Next Chapter（下一章）：[]()**
