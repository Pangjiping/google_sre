## **Configuration Management**

## **配置管理**

Configuration management is one area of particularly close collaboration between release engineers and SREs. Although configuration management may initially seem a deceptively simple problem, configuration changes are a potential source of instability. As a result, our approach to releasing and managing system and service configurations has evolved substantially over time. Today we use several models for distributing configuration files, as described in the following paragraphs. All schemes involve storing configuration in our primary source code repository and enforcing a strict code review requirement.

配置管理是发布工程师和SRE之间密切合作的领域之一。尽管配置管理最初看起来似乎是一个简单的问题，但配置更改是潜在的不稳定源。因此，我们发布和管理系统和服务配置的方法随着时间的推移发生了重大变化。今天我们使用几种模型来分发配置文件，如下文所述。所有方案都涉及将配置存储在我们的主要源代码存储库中，并执行严格的代码审查要求。

**Use the mainline for configuration**. This was the first method used to configure services in Borg (and the systems that pre-dated Borg). Using this scheme, developers and SREs modify configuration files at the head of the main branch. The changes are reviewed and then applied to the running system. As a result, binary releases and configuration changes are decoupled. While conceptually and procedurally simple, this technique often leads to skew between the checked-in version of the configuration files and the running version of the configuration file because jobs must be updated in order to pick up the changes.

**使用主线进行配置。**这是用于在Borg中配置服务的第一种方法。使用这种方案，开发人员和SRE在主分支修改配置文件。检查更改，然后将其应用于正在运行的系统。因此，二进制版本和配置更改是分离的。虽然在概念上和程序上都很简单，但这种技术通常会导致配置文件的签入版本和配置文件的运行版本之间出现偏差，因为必须更新作业才能获取更改。

**Include configuration files and binaries in the same MPM package**. For projects with few configuration files or projects where the files (or a subset of files) change with each release cycle, the configuration files can be included in the MPM package with the binaries. While this strategy limits flexibility by binding the binary and configuration files tightly, it simplifies deployment, because it only requires installing one package.

**在同一个MPM包中包含配置文件和二进制文件。**对于配置文件很少的项目或文件和随每个发布周期而变化的项目，配置文件可以与二进制文件一起包含在MPM包中。虽然这种策略通过将二进制文件和配置文件紧密绑定来限制灵活性，但它简化了部署，因为它只需要安装一个包。

**Package configuration files into MPM "configuration packages."** We can apply the hermetic principle to configuration management. Binary configurations tend to be tightly bound to particular versions of binaries, so we leverage the build and packaging systems to snapshot and release configuration files alongside their binaries. Similar to our treatment of binaries, we can use the build ID to reconstruct the configuration at a specific point in time.

**将配置文件打包到MPM“配置包”中。**我们可以将封闭原则应用于配置管理。二进制配置往往与特定版本的二进制文件紧密绑定，因此我们利用构建和打包系统来快照和发布配置文件及其二进制文件。类似于我们对二进制文件的处理，我们可以使用构建ID来重建特定时间点的配置。

For example, a change that implements a new feature can be released with a flag setting that configures that feature. By generating two MPM packages, one for the binary and one for the configuration, we retain the ability to change each package independently. That is, if the feature was released with a flag setting of first_folio but we realize it should instead be bad_quarto, we can cherry pick that change onto the release branch, rebuild the configuration package, and deploy it. This approach has the advantage of not requiring a new binary build.

例如，可以使用配置该功能的标志设置来发布实现新功能的更改。通过生成两个MPM包，一个用于二进制文件，一个用于配置，我们保留了独立更改每个包的能力。也就是说，如果该功能是使用`first_folio`标志设置发布的，但我们意识到它应该改为`bad_quarto`，我们可以将该更改合并到发布分支上，重建配置包，然后部署它。这种方法的优点是不需要新的二进制构建。

We can leverage MPM’s labeling feature to indicate which versions of MPM packages should be installed together. A label of much_ado can be applied to the MPM packages described in the previous paragraph, which allows us to fetch both packages using this label. When a new version of the project is built, the much_ado label will be applied to the new packages. Because these tags are unique within the namespace for an MPM package, only the latest package with that tag will be used.

我们可以利用MPM的标签功能来指示应该一起安装哪些版本的MPM包。可以将`much_ado`标签应用于上一段中描述的MPM包，这使我们可以使用此标签获取两个包。当构建项目的新版本时，`much_ado`标签将应用于新包。因为这些标签在MPM包的命名空间中是唯一的，所以只会使用带有该标签的最新包。

**Read configuration files from an external store**. Some projects have configuration files that need to change frequently or dynamically (i.e., while the binary is running). These files can be stored in Chubby, Bigtable, or our source-based filesystem [Kem11].

**从外部存储读取配置文件。**某些项目的配置文件需要经常或动态更改。这些文件可以存储在Chubby、Bigtable或我们基于源代码的文件系统 [Kem11] 中。

In summary, project owners consider the different options for distributing and managing configuration files and decide which works best on a case-by-case basis.

总而言之，项目所有者会考虑用于分发和管理配置文件的不同选项，并根据具体情况决定哪种方式最有效。
