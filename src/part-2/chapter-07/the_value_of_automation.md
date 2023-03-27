## **The Value of Automation**

## **自动化的价值**

What exactly is the value of automation?

自动化的价值究竟是什么？

<br>

### **Consistency**

### **一致性**

Although scale is an obvious motivation for automation, there are many other reasons to use it. Take the example of university computing systems, where many systems engineering folks started their careers. Systems administrators of that background were generally charged with running a collection of machines or some software, and were accustomed to manually performing various actions in the discharge of that duty. One common example is creating user accounts; others include purely operational duties like making sure backups happen, managing server failover, and small data manipulations like changing the upstream DNS servers’ resolv.conf, DNS server zone data, and similar activities. Ultimately, however, this prevalence of manual tasks is unsatisfactory for both the organizations and indeed the people maintaining systems in this way. For a start, any action performed by a human or humans hundreds of times won’t be performed the same way each time: even with the best will in the world, very few of us will ever be as consistent as a machine. This inevitable lack of consistency leads to mistakes, oversights, issues with data quality, and, yes, reliability problems. In this domain—the execution of well-scoped, known procedures—the value of consistency is in many ways the primary value of automation.

虽然规模是自动化的一个明显的动机，但还有许多其他的理由来使用它。以大学计算机系统为例，许多系统工程人员在那里开始他们的职业生涯。那种背景的系统管理员通常负责运行一组机器或一些软件，并习惯于在履行这一职责时手动执行各种操作。一个常见的例子是创建用户账户；其他包括纯粹的运维职责，如确保备份，管理服务器故障转移，以及小的数据操作，如改变上游DNS服务器的resolv.conf、DNS服务器区域数据，以及类似的活动。然而最终，这种手工任务的盛行对组织和以这种方式维护系统的人来说都是不满意的。首先，由人或人类执行的任何行动，每次都不会以相同的方式进行：即使有世界上最好的愿景，我们中很少有人会像机器那样一致。这种不可避免的一致性缺乏会导致错误、疏忽、数据质量问题，以及可靠性问题。在这个领域--执行范围明确的、已知的程序--一致性的价值在许多方面是自动化的主要价值。

<br>

### **A Platform**

### **一个平台**

Automation doesn’t just provide consistency. Designed and done properly, automatic systems also provide a platform that can be extended, applied to more systems, or perhaps even spun out for profit. (The alternative, no automation, is neither cost effective nor extensible: it is instead a tax levied on the operation of a system.)

自动化不只是提供一致性。如果设计和操作得当，自动系统也提供了一个可以扩展的平台，可以应用于更多的系统，甚至可能被剥离出来盈利。（另一种选择，没有自动化，既不符合成本效益，也不能扩展：而是对系统的运行征税）。

A platform also centralizes mistakes. In other words, a bug fixed in the code will be fixed there once and forever, unlike a sufficiently large set of humans performing the same procedure, as discussed previously. A platform can be extended to perform additional tasks more easily than humans can be instructed to perform them (or sometimes even realize that they have to be done). Depending on the nature of the task, it can run either continuously or much more frequently than humans could appropriately accomplish the task, or at times that are inconvenient for humans. Furthermore, a platform can export metrics about its performance, or otherwise allow you to discover details about your process you didn’t know previously, because these details are more easily measurable within the context of a platform.

一个平台也集中了错误。换句话说，在代码中修复的错误将在那里被永远修复，而不像前面讨论的那样，由足够多的人类执行相同的程序。一个平台可以被扩展到执行更多的任务，比人类执行这些任务（有时甚至意识到必须要做这些任务）更容易。根据任务的性质，它可以连续运行，或者比人类完成任务的频率高得多，或者在人类不方便的时候运行。此外，一个平台可以输出有关其性能的指标，或以其他方式让你发现你以前不知道的流程细节，因为这些细节在一个平台的背景下更容易衡量。

<br>

### **Faster Repairs**

### **更快地修复**

There’s an additional benefit for systems where automation is used to resolve common faults in a system (a frequent situation for SRE-created automation). If automation runs regularly and successfully enough, the result is a reduced mean time to repair (MTTR) for those common faults. You can then spend your time on other tasks instead, thereby achieving increased developer velocity because you don’t have to spend time either preventing a problem or (more commonly) cleaning up after it.

对于用于解决系统中的常见故障的自动化系统，还有一个额外的好处（这是SRE创建的自动化经常出现的情况）。如果自动化定期运行并足够成功，其结果是减少了这些常见故障的平均修复时间（MTTR）。然后，你可以把时间花在其他任务上，从而实现提高开发人员的速度，因为你不必花时间去防止问题或清理问题。

As is well understood in the industry, the later in the product lifecycle a problem is discovered, the more expensive it is to fix; see Chapter 17. Generally, problems that occur in actual production are most expensive to fix, both in terms of time and money, which means that an automated system looking for problems as soon as they arise has a good chance of lowering the total cost of the system, given that the system is sufficiently large.

正如业内人士所了解的那样，在产品生命周期的后期发现问题，修复的成本就越高；见17章。一般来说，在实际生产中发生的问题在时间和金钱上都是最昂贵的，这意味着只要系统足够大，一个自动系统在问题出现时立即寻找问题，就有很大机会降低系统的总成本。

<br>

### **Faster Action**

### **更快地行动**

In the infrastructural situations where SRE automation tends to be deployed, humans don’t usually react as fast as machines. In most common cases, where, for example, failover or traffic switching can be well defined for a particular application, it makes no sense to effectively require a human to intermittently press a button called "Allow system to continue to run." (Yes, it is true that sometimes automatic procedures can end up making a bad situation worse, but that is why such procedures should be scoped over well-defined domains.) Google has a large amount of automation; in many cases, the services we support could not long survive without this automation because they crossed the threshold of manageable manual operation long ago.

在倾向于部署SRE自动化的基础设施情况下，人类通常不会像机器那样快速反应。在大多数常见的情况下，例如，故障转移或流量切换可以为一个特定的应用程序很好地定义，有效地要求人类间歇性地按下一个名为“允许系统继续运行”的按钮是毫无意义的。(是的，有时自动程序确实会使糟糕的情况最终变得更糟，但这就是为什么这种程序应该在定义明确的领域内进行范围化的原因。) Google有大量的自动化；在许多情况下，如果没有这种自动化，我们支持的服务不可能长期运行，因为它们早就越过了可管理的手工运维的阈值。

<br>

### **Time Saving**

### **节省时间**

Finally, time saving is an oft-quoted rationale for automation. Although people cite this rationale for automation more than the others, in many ways the benefit is often less immediately calculable. Engineers often waver over whether a particular piece of automation or code is worth writing, in terms of effort saved in not requiring a task to be performed manually versus the effort required to write it. It’s easy to overlook the fact that once you have encapsulated some task in automation, anyone can execute the task. Therefore, the time savings apply across anyone who would plausibly use the automation. Decoupling operator from operation is very powerful.

最后，节省时间是一个经常被引用的自动化的理由。虽然人们引用这个自动化的理由比其他理由多，但在许多方面的好处往往不容易立即计算出来。工程师们经常为某一特定的自动化或代码是否值得编写而摇摆不定。从不需要手动执行的任务所节省的精力与编写任务所需的精力来看，节省的时间适用于任何有可能使用自动化的人。将运维人员与运维任务脱钩是非常强大的。

<br>

---

**[Back to contents of the chapter（返回章节目录）](the_evolution_of_automation_at_google.md)**

* **Next Section（下一节）：[The Value for Google SRE（Google SRE的价值）](the_value_of_google_sre.md)**
