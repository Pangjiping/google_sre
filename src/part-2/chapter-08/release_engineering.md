# **Release Engineering**

# **发布工程**

> Written by Dinah McNutt
>
> Edited by Betsy Beyer and Tim Harvey

Release engineering is a relatively new and fast-growing discipline of software engineering that can be concisely described as building and delivering software [[McN14a]](https://www.usenix.org/system/files/login/articles/05_mcnutt.pdf). Release engineers have a solid (if not expert) understanding of source code management, compilers, build configuration languages, automated build tools, package managers, and installers. Their skill set includes deep knowledge of multiple domains: development, configuration management, test integration, system administration, and customer support.

发布工程是软件工程中一门相对较新且发展迅速的学科，可以简明地描述为构建和交付软件 [[McN14a]](https://www.usenix.org/system/files/login/articles/05_mcnutt.pdf)。发布工程师对源代码管理、编译器、构建配置语言、自动构建工具、软件包管理器和安装程序有扎实的了解。他们的技能组合包括多个领域的深刻知识：开发、配置管理、测试集成、系统管理和客户支持。

Running reliable services requires reliable release processes. Site Reliability Engineers (SREs) need to know that the binaries and configurations they use are built in a reproducible, automated way so that releases are repeatable and aren’t "unique snowflakes." Changes to any aspect of the release process should be intentional, rather than accidental. SREs care about this process from source code to deployment.

运行可靠的服务需要可靠的发布过程。SRE需要知道他们使用的二进制文件和配置是以可重现的自动化方式构建的，以便发布是可重复的，而不是“独特的雪花”。对发布过程的任何方面的更改都应该是有意的，而不是偶然的。SRE关心从源代码到部署的这个过程。

Release engineering is a specific job function at Google. Release engineers work with software engineers (SWEs) in product development and SREs to define all the steps required to release software—from how the software is stored in the source code repository, to build rules for compilation, to how testing, packaging, and deployment are conducted.

发布工程是Google的一项特定工作。发布工程师与产品开发和SRE中的软件工程师 (SWE) 合作，定义发布软件所需的所有步骤——从软件如何存储在代码存储库中，到构建编译规则，再到如何测试、打包和部署。

- [The Role of a Release Engineer（发布工程师的角色）](the_role_of_a_release_engineer.md)
- [Philosophy（理念）](philosophy.md)
- [Continuous Build and Deployment（持续集成和部署）](continuous_build_and_deployment.md)
- [Configuration Management（配置管理）](configuration_management.md)
- [Conclusions（总结）](conclusions.md)
