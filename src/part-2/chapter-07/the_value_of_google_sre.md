## **The Value for Google SRE**

## **Google SRE的价值**

All of these benefits and trade-offs apply to us just as much as anyone else, and Google does have a strong bias toward automation. Part of our preference for automation springs from our particular business challenges: the products and services we look after are planet-spanning in scale, and we don’t typically have time to engage in the same kind of machine or service hand-holding common in other organizations. For truly large services, the factors of consistency, quickness, and reliability dominate most conversations about the trade-offs of performing automation.

所有这些自动化的好处和权衡都适用于我们，而Google确实对自动化有强烈的偏爱。我们对自动化的偏爱部分来自于我们特殊的业务挑战：我们负责的产品和服务在规模上是跨越全球的，我们通常没有时间参与其他组织常见的那种机器或服务的指导。

Another argument in favor of automation, particularly in the case of Google, is our complicated yet surprisingly uniform production environment, described in Chapter 2. While other organizations might have an important piece of equipment without a readily accessible API, software for which no source code is available, or another impediment to complete control over production operations, Google generally avoids such scenarios. We have built APIs for systems when no API was available from the vendor. Even though purchasing software for a particular task would have been much cheaper in the short term, we chose to write our own solutions, because doing so produced APIs with the potential for much greater long-term benefits. We spent a lot of time overcoming obstacles to automatic system management, and then resolutely developed that automatic system management itself. Given how Google manages its source code [[Pot16]](https://www.youtube.com/watch?v=W71BTkUbdqE), the availability of that code for more or less any system that SRE touches also means that our mission to "own the product in production" is much easier because we control the entirety of the stack.

另一个支持自动化的论点，特别是在Google的情况下，是我们复杂但令人惊讶的统一生产环境，在[第2章](../../part-1/chapter-02/the_production_environment_at_google_from_the_viewpoint_of_an_sre.md)中描述。虽然其他组织可能有一个重要的设备没有现成的API，软件没有源代码，或其他阻碍完全控制生产操作的因素，但Google通常避免这种情况。在供应商没有提供API的情况下，我们已经为系统建立了API。即使为某一特定任务购买软件在短期内会便宜得多，我们还是选择自己编写解决方案，因为这样做产生的API有可能带来更大的长期利益。我们花了很多时间来克服自动系统管理的障碍，然后坚定地开发自动系统管理本身。鉴于Google是如何管理其源代码的[[Pot16]](https://www.youtube.com/watch?v=W71BTkUbdqE)，SRE所接触到的任何系统都可以获得这些代码，这也意味着我们“在生产中拥有产品”的使命要容易得多，因为我们控制着整个过程。

Of course, although Google is ideologically bent upon using machines to manage machines where possible, reality requires some modification of our approach. It isn’t appropriate to automate every component of every system, and not everyone has the ability or inclination to develop automation at a particular time. Some essential systems started out as quick prototypes, not designed to last or to interface with automation. The previous paragraphs state a maximalist view of our position, but one that we have been broadly successful at putting into action within the Google context. In general, we have chosen to create platforms where we could, or to position ourselves so that we could create platforms over time. We view this platform-based approach as necessary for manageability and scalability.

当然，尽管Google在意识形态上倾向于在可能的情况下使用机器来管理机器，但现实要求我们对方法进行一些修改。把每个系统的每个组件都自动化是不合适的，而且不是每个人都有能力或倾向于在特定的时间发展自动化。一些基本的系统一开始就是快速的原型，并不是为了持久或与自动化对接而设计的。前面几段陈述了我们的立场，但我们在Google的背景下已经大致成功地将其付诸行动了。总的来说，我们选择了在我们能够做到的地方构建自动化平台，或者将我们自己定位为能够随着时间的推移而构建。我们认为这种基于平台的方法对于可管理性和可扩展性是必要的。

<br>

---

**[Back to contents of the chapter（返回章节目录）](the_evolution_of_automation_at_google.md)**

* **Previous Section（上一节）：[The Value of Automation（自动化的价值）](the_value_of_automation.md)**
* **Next Section（下一节）：[The Use Cases for Automation（使用自动化的例子）](the_use_cases_for_automation.md)**
