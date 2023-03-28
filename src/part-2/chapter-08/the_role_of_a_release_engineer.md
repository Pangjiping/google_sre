## **The Role of a Release Engineer**

## **发布工程师的角色**

Google is a data-driven company and release engineering follows suit. We have tools that report on a host of metrics, such as how much time it takes for a code change to be deployed into production (in other words, release velocity) and statistics on what features are being used in build configuration files [[Ada15]](http://resources.sei.cmu.edu/library/asset-view.cfm?assetid=434819). Most of these tools were envisioned and developed by release engineers.

谷歌是一家数据驱动的公司，发布工程也是如此。我们有报告大量指标的工具，例如发布速度以及有关构建配置文件中使用的功能的统计信息 [[Ada15]](http://resources.sei.cmu.edu/library/asset-view.cfm?assetid=434819)。这些工具中的大多数都是由发布工程师设计和开发的。

Release engineers define best practices for using our tools in order to make sure projects are released using consistent and repeatable methodologies. Our best practices cover all elements of the release process. Examples include compiler flags, formats for build identification tags, and required steps during a build. Making sure that our tools behave correctly by default and are adequately documented makes it easy for teams to stay focused on features and users, rather than spending time reinventing the wheel (poorly) when it comes to releasing software.

发布工程师定义使用我们工具的最佳实践，以确保使用一致且可重复的方法发布项目。我们的最佳实践涵盖发布过程的所有要素。包括编译器标志、构建标识标签的格式以及构建过程中所需的步骤。确保我们的工具在默认情况下正确运行并有充分的文档记录，使团队可以轻松地专注于功能和用户，而不是在发布软件时花时间重新发明轮子。

Google has a large number of SREs who are charged with safely deploying products and keeping Google services up and running. In order to make sure our release processes meet business requirements, release engineers and SREs work together to develop strategies for canarying changes, pushing out new releases without interrupting services, and rolling back features that demonstrate problems.

Google拥有大量SRE，他们负责安全部署产品并保持Google服务正常运行。为了确保我们的发布流程满足业务需求，发布工程师和SRE共同制定金丝雀变更策略，在不中断服务的情况下推出新版本，并回滚出现问题的功能。
