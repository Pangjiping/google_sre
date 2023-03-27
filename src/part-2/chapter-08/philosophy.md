## **Philosophy**

Release engineering is guided by an engineering and service philosophy that’s expressed through four major principles, detailed in the following sections.

<br>

### **Self-Service Model**

In order to work at scale, teams must be self-sufficient. Release engineering has developed best practices and tools that allow our product development teams to control and run their own release processes. Although we have thousands of engineers and products, we can achieve a high release velocity because individual teams can decide how often and when to release new versions of their products. Release processes can be automated to the point that they require minimal involvement by the engineers, and many projects are automatically built and released using a combination of our automated build system and our deployment tools. Releases are truly automatic, and only require engineer involvement if and when problems arise.

<br>

### **High Velocity**

User-facing software (such as many components of Google Search) is rebuilt frequently, as we aim to roll out customer-facing features as quickly as possible. We have embraced the philosophy that frequent releases result in fewer changes between versions. This approach makes testing and troubleshooting easier. Some teams perform hourly builds and then select the version to actually deploy to production from the resulting pool of builds. Selection is based upon the test results and the features contained in a given build. Other teams have adopted a "Push on Green" release model and deploy every build that passes all tests [Kle14].

<br>

### **Hermetic Builds**

Build tools must allow us to ensure consistency and repeatability. If two people attempt to build the same product at the same revision number in the source code repository on different machines, we expect identical results.1 Our builds are hermetic, meaning that they are insensitive to the libraries and other software installed on the build machine. Instead, builds depend on known versions of build tools, such as compilers, and dependencies, such as libraries. The build process is self-contained and must not rely on services that are external to the build environment.

Rebuilding older releases when we need to fix a bug in software that’s running in production can be a challenge. We accomplish this task by rebuilding at the same revision as the original build and including specific changes that were submitted after that point in time. We call this tactic cherry picking. Our build tools are themselves versioned based on the revision in the source code repository for the project being built. Therefore, a project built last month won’t use this month’s version of the compiler if a cherry pick is required, because that version may contain incompatible or undesired features.

<br>

### **Enforcement of Policies and Procedures**

Several layers of security and access control determine who can perform specific operations when releasing a project. Gated operations include:

* Approving source code changes—this operation is managed through configuration files scattered throughout the codebase
* Specifying the actions to be performed during the release process
* Creating a new release
* Approving the initial integration proposal (which is a request to perform a build at a specific revision number in the source code repository) and subsequent cherry picks
* Deploying a new release
* Making changes to a project’s build configuration

Almost all changes to the codebase require a code review, which is a streamlined action integrated into our normal developer workflow. Our automated release system produces a report of all changes contained in a release, which is archived with other build artifacts. By allowing SREs to understand what changes are included in a new release of a project, this report can expedite troubleshooting when there are problems with a release.
