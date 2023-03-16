## **Toil Defined**

## **劳作的定义**

Toil is not just "work I don’t like to do." It’s also not simply equivalent to administrative chores or grungy work. Preferences as to what types of work are satisfying and enjoyable vary from person to person, and some people even enjoy manual, repetitive work. There are also administrative chores that have to get done, but should not be categorized as toil: this is overhead. Overhead is often work not directly tied to running a production service, and includes tasks like team meetings, setting and grading goals, snippets, and HR paperwork. Grungy work can sometimes have long-term value, and in that case, it’s not toil, either. Cleaning up the entire alerting configuration for your service and removing clutter may be grungy, but it’s not toil.

劳作不仅仅是“我不喜欢做的工作”。它也不简单地等同于行政杂务或枯燥的工作。对于什么类型的工作是令人满意和愉快的，每个人的偏好都不同，有些人甚至喜欢手工、重复性的工作。还有一些必须完成的行政杂务，但不应该被归类为劳作：这就是间接费用。间接费用通常是与经营生产服务没有直接联系的工作，包括团队会议、设定和评定目标、人力资源文书工作等任务。琐碎的工作有时会有长期的价值，在这种情况下，它也不是劳作。清理你的服务的整个警报配置，清除杂乱无章的东西，这可能是枯燥的，但不是劳作。

So what is toil? Toil is the kind of work tied to running a production service that tends to be manual, repetitive, automatable, tactical, devoid of enduring value, and that scales linearly as a service grows. Not every task deemed toil has all these attributes, but the more closely work matches one or more of the following descriptions, the more likely it is to be toil:

* **Manual**. This includes work such as manually running a script that automates some task. Running a script may be quicker than manually executing each step in the script, but the hands-on time a human spends running that script (not the elapsed time) is still toil time.
* **Repetitive**. If you’re performing a task for the first time ever, or even the second time, this work is not toil. Toil is work you do over and over. If you’re solving a novel problem or inventing a new solution, this work is not toil.
* **Automatable**. If a machine could accomplish the task just as well as a human, or the need for the task could be designed away, that task is toil. If human judgment is essential for the task, there’s a good chance it’s not toil.
* **Tactical**. Toil is interrupt-driven and reactive, rather than strategy-driven and proactive. Handling pager alerts is toil. We may never be able to eliminate this type of work completely, but we have to continually work toward minimizing it.
* **No enduring value**. If your service remains in the same state after you have finished a task, the task was probably toil. If the task produced a permanent improvement in your service, it probably wasn’t toil, even if some amount of grunt work—such as digging into legacy code and configurations and straightening them out—was involved.
* **O(n) with service growth**. If the work involved in a task scales up linearly with service size, traffic volume, or user count, that task is probably toil. An ideally managed and designed service can grow by at least one order of magnitude with zero additional work, other than some one-time efforts to add resources.

那么，什么是劳作？劳作是与运行生产服务相关的那种工作，往往是手动的、重复的、可自动化的、战术性的、没有持久价值的，并且随着服务的增长而线性扩展。并非每项被认为是劳作的任务都具有所有这些属性，但工作越是符合以下一项或多项描述，就越有可能是劳作：

* **手动**。这包括一些工作，如手动运行一个自动完成某些任务的脚本。运行一个脚本可能比手动执行脚本中的每一步要快，但人在运行该脚本时所花费的实践时间（而不是经过的时间）仍然是劳作时间。
* **重复性**。如果你是第一次执行一项任务，甚至是第二次，这项工作就不是劳作。劳作是你反复做的工作。如果你正在解决一个新的问题或发明一个新的解决方案，这项工作就不是劳作。
* **可自动化**。如果机器可以和人一样好地完成任务，或者任务的需要可以被设计出来，那么这个任务就是劳作。如果人类的判断力对于这项任务来说是必不可少的，那么很有可能它就不是劳作。

<br>

---

**[Back to contents of the chapter（返回章节目录）](eliminating_toil.md)**

* **Next Section（下一节）：[Why Less Toil Is Better（为什么更少的劳作更好）](why_less_toil_is_better.md)**
