## **Conclusions**

While this chapter has specifically discussed Google’s approach to release engineering and the ways in which release engineers work and collaborate with SREs, these practices can also be applied more widely.

<br>

### **It’s Not Just for Googlers**

When equipped with the right tools, proper automation, and well-defined policies, developers and SREs shouldn’t have to worry about releasing software. Releases can be as painless as simply pressing a button.

Most companies deal with the same set of release engineering problems regardless of their size or the tools they use: How should you handle versioning of your packages? Should you use a continuous build and deploy model, or perform periodic builds? How often should you release? What configuration management policies should you use? What release metrics are of interest?

Google Release Engineers have developed our own tools out of necessity because open sourced or vendor-supplied tools don’t work at the scale we require. Custom tools allow us to include functionality to support (and even enforce) release process policies. However, these policies must first be defined in order to add appropriate features to our tools, and all companies should take the effort to define their release processes whether or not the processes can be automated and/or enforced.

<br>

### **Start Release Engineering at the Beginning**

Release engineering has often been an afterthought, and this way of thinking must change as platforms and services continue to grow in size and complexity.

Teams should budget for release engineering resources at the beginning of the product development cycle. It’s cheaper to put good practices and process in place early, rather than have to retrofit your system later.

It is essential that the developers, SREs, and release engineers work together. The release engineer needs to understand the intention of how the code should be built and deployed. The developers shouldn’t build and "throw the results over the fence" to be handled by the release engineers.

Individual project teams decide when release engineering becomes involved in a project. Because release engineering is still a relatively young discipline, managers don’t always plan and budget for release engineering in the early stages of a project. Therefore, when considering how to incorporate release engineering practices, be sure that you consider its role as applied to the entire lifecycle of your product or service—particularly the early stages.

<br>

> More Information
>
> For more information on release engineering, see the following presentations, each of which has video available online:
>
> * [How Embracing Continuous Release Reduced Change Complexity](https://www.usenix.org/conference/ures14west/summit-program/presentation/dickson), USENIX Release Engineering Summit West 2014, [[Dic14]](http://usenix.org/conference/ures14west/summit-program/presentation/dickson)
> * [Maintaining Consistency in a Massively Parallel Environment](https://www.usenix.org/conference/ucms13/summit-program/presentation/mcnutt), USENIX Configuration Management Summit 2013, [[McN13]](https://www.usenix.org/conference/ucms13/summit-program/presentation/mcnutt)
> * [The 10 Commandments of Release Engineering](https://www.youtube.com/watch?v=RNMjYV_UsQ8), 2nd International Workshop on Release Engineering 2014, [[McN14b]](https://www.youtube.com/watch?v=RNMjYV_UsQ8)
> * [Distributing Software in a Massively Parallel Environment](https://www.usenix.org/conference/lisa14/conference-program/presentation/mcnutt), LISA 2014, [[McN14c]](https://www.usenix.org/conference/lisa14/conference-program/presentation/mcnutt)
