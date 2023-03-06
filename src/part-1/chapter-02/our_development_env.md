## **Our Development Environment**

## **开发环境**

Development velocity is very important to Google, so we’ve built a complete development environment to make use of our infrastructure [[Mor12b]](https://research.google.com/pubs/pub37755.html).

开发速度对于谷歌非常重要，因此我们构建了一个完整的开发环境来利用我们的基础设施[[Mor12b]](https://research.google.com/pubs/pub37755.html)。

Apart from a few groups that have their own open source repositories (e.g., Android and Chrome), Google Software Engineers work from a single shared repository [[Pot16]](https://www.youtube.com/watch?v=W71BTkUbdqE). This has a few important practical implications for our workflows:

* If engineers encounter a problem in a component outside of their project, they can fix the problem, send the proposed changes (“changelist,” or CL) to the owner for review, and submit the CL to the mainline.
* Changes to source code in an engineer’s own project require a review. All software is reviewed before being submitted.

除了一些具有自己的开源代码库（例如Android和Chrome）的小组之外，Google的软件工程师都是从一个单一的共享代码库 [[Pot16]](https://www.youtube.com/watch?v=W71BTkUbdqE) 中工作的。这对我们的工作流程有一些重要的实际影响：

* 如果工程师在其项目之外的组件中遇到问题，他们可以修复该问题，将所提议的变更（称为“变更列表”或CL）发送给所有者进行审核，并将CL提交到主干。
* 对于一个工程师自己项目中源代码的变更，需要进行审查。所有的软件都需要在提交之前进行审查。

When software is built, the build request is sent to build servers in a datacenter. Even large builds are executed quickly, as many build servers can compile in parallel. This infrastructure is also used for continuous testing. Each time a CL is submitted, tests run on all software that may depend on that CL, either directly or indirectly. If the framework determines that the change likely broke other parts in the system, it notifies the owner of the submitted change. Some projects use a push-on-green system, where a new version is automatically pushed to production after passing tests.

当软件进行构建时，构建请求会被发送到数据中心中的构建服务器。即使是大型构建也可以快速执行，因为许多构建服务器可以并行编译。这种基础设施也用于持续测试。每次提交CL时，测试都会在所有可能依赖于该CL的软件上运行，无论是直接还是间接的。如果框架确定更改可能会破坏系统中的其他部分，则会通知提交更改的所有者。有些项目使用“在绿色环境中推送”的系统，即在通过测试后自动将新版本推送到生产环境。

<br>

---

**[Back to contents of the chapter（返回章节目录）](the_production_environment_at_google_from_the_viewpoint_of_an_sre.md)**

* **Previous Section（上一节）：[Our Software Infrastructure（软件基础设施）](our_software_infra.md)**
* **Next Section（下一节）：[Shakespeare: A Sample Service（Shakespeare：一个示例服务）](shakespare_a_simple_service.md)**
