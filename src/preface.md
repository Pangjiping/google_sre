# **Preface**

# **序言**

Software engineering has this in common with having children: the labor before the birth is painful and difficult, but the labor after the birth is where you actually spend most of your effort. Yet software engineering as a discipline spends much more time talking about the first period as opposed to the second, despite estimates that 40–90% of the total costs of a system are incurred after birth. The popular industry model that conceives of deployed, operational software as being “stabilized” in production, and therefore needing much less attention from software engineers, is wrong. Through this lens, then, we see that if software engineering tends to focus on designing and building software systems, there must be another discipline that focuses on the whole lifecycle of software objects, from inception, through deployment and operation, refinement, and eventual peaceful decommissioning. This discipline uses—and needs to use—a wide range of skills, but has separate concerns from other kinds of engineers. Today, our answer is the discipline Google calls Site Reliability Engineering.

软件工程与生孩子有共同点：出生前的劳动是痛苦和困难的，但出生后的劳动才是你实际上花费大部分精力的地方。然而，尽管估计系统总成本的40-90%是在出生后产生的，软件工程作为一门学科却花费更多时间谈论第一阶段而不是第二阶段。流行的行业模式认为，在生产中部署、运行的软件被视为“稳定”，因此需要软件工程师的关注要少得多，这是错误的。因此，我们可以看到，如果软件工程倾向于关注设计和构建软件系统，那么必须有另一门学科专注于软件对象的整个生命周期，从构思、部署和运营，到改进，最终的平滑退役。这门学科使用并需要使用广泛的技能，但与其他类型的工程师有着不同的问题。今天，我们的答案是Google所称的站点可靠性工程（SRE）学科。

So what exactly is Site Reliability Engineering (SRE)? We admit that it’s not a particularly clear name for what we do—pretty much every site reliability engineer at Google gets asked what exactly that is, and what they actually do, on a regular basis.

那么什么是SRE？我们承认这并不是一个非常清晰的名称来描述我们的工作——几乎每个在谷歌担任站点可靠性工程师的人都经常被问及究竟是什么以及他们实际上做些什么。

Unpacking the term a little, first and foremost, SREs are engineers. We apply the principles of computer science and engineering to the design and development of computing systems: generally, large distributed ones. Sometimes, our task is writing the software for those systems alongside our product development counterparts; sometimes, our task is building all the additional pieces those systems need, like backups or load balancing, ideally so they can be reused across systems; and sometimes, our task is figuring out how to apply existing solutions to new problems.

稍微解释一下这个术语，首先，SRE是工程师。我们将计算机科学和工程学原理应用于计算系统的设计和开发中，通常是大型分布式系统。有时，我们的任务是与我们的产品开发同事一起编写这些系统的软件；有时，我们的任务是构建这些系统需要的所有附加组件，如备份或负载均衡，以便它们可以在系统之间重复使用；有时，我们的任务是找出如何将现有解决方案应用于新问题。

Next, we focus on system reliability. Ben Treynor Sloss, Google’s VP for 24/7 Operations, originator of the term SRE, claims that reliability is the most fundamental feature of any product: a system isn’t very useful if nobody can use it! Because reliability2 is so critical, SREs are focused on finding ways to improve the design and operation of systems to make them more scalable, more reliable, and more efficient. However, we expend effort in this direction only up to a point: when systems are “reliable enough,” we instead invest our efforts in adding features or building new products.

接下来，我们关注系统的可靠性。Google的全天候运营副总裁，SRE术语的发起人Ben Treynor Sloss认为，可靠性是任何产品最基本的特征：如果没有人能使用它，那么系统就没有什么用处！因为可靠性非常关键，SRE专注于找到改善系统设计和操作的方法，使其更可扩展、更可靠和更高效。但是，我们只会在这个方向上投入一定的努力：当系统变得“足够可靠”时，我们将投入努力来添加功能或构建新产品。

Finally, SREs are focused on operating services built atop our distributed computing systems, whether those services are planet-scale storage, email for hundreds of millions of users, or where Google began, web search. The “site” in our name originally referred to SRE’s role in keeping the google.com website running, though we now run many more services, many of which aren’t themselves websites—from internal infrastructure such as Bigtable to products for external developers such as the Google Cloud Platform.

最后，SRE专注于在我们的分布式计算系统之上运行服务，无论这些服务是面向全球的存储、数亿用户的电子邮件，还是Google的起点——Web搜索。我们名字中的“站点”最初指的是SRE在维护google.com网站方面的角色，尽管我们现在运行的服务更多，其中许多并不是网站——从像Bigtable这样的内部基础设施到面向外部开发人员的产品，如Google Cloud Platform。

Although we have represented SRE as a broad discipline, it is no surprise that it arose in the fast-moving world of web services, and perhaps in origin owes something to the peculiarities of our infrastructure. It is equally no surprise that of all the postdeployment characteristics of software that we could choose to devote special attention to, reliability is the one we regard as primary. The domain of web services, both because the process of improving and changing server-side software is comparatively contained, and because managing change itself is so tightly coupled with failures of all kinds, is a natural platform from which our approach might emerge.

虽然我们已经将SRE描述成一门广泛的学科，但它在快速发展的Web服务领域出现并不奇怪，或许起源于我们基础设施的特殊性质。同样不足为奇的是，在所有可选择关注的软件部署后特性中，我们将可靠性视为首要特性。Web服务领域之所以成为我们方法出现的自然平台，一方面是因为改进和更改服务器端软件的过程相对容易掌控，另一方面是因为管理变更本身与各种失败紧密相连。

Despite arising at Google, and in the web community more generally, we think that this discipline has lessons applicable to other communities and other organizations. This book is an attempt to explain how we do things: both so that other organizations might make use of what we’ve learned, and so that we can better define the role and what the term means. To that end, we have organized the book so that general principles and more specific practices are separated where possible, and where it’s appropriate to discuss a particular topic with Google-specific information, we trust that the reader will indulge us in this and will not be afraid to draw useful conclusions about their own environment.

虽然SRE起源于Google和Web社区，但我们认为这门学科的经验可以应用于其他社区和组织。本书旨在解释我们如何做事情：一方面让其他组织可以利用我们所学到的知识，另一方面也更好地定义这个角色和这个术语的含义。为此，我们将本书组织成通用原则和更具体的实践分开讨论，必要时讨论特定主题时涉及到谷歌的信息，我们相信读者会容忍我们这样做，并会毫不犹豫地从自己的环境中得出有用的结论。

We have also provided some orienting material—a description of Google’s production environment and a mapping between some of our internal software and publicly available software—which should help to contextualize what we are saying and make it more directly usable.

我们还提供了一些指导材料——对Google的生产环境的描述和一些我们内部软件和公开可用软件之间的映射，这应该有助于将我们所说的内容放入背景中，并使其更直接可用。

Ultimately, of course, more reliability-oriented software and systems engineering is inherently good. However, we acknowledge that smaller organizations may be wondering how they can best use the experience represented here: much like security, the earlier you care about reliability, the better. This implies that even though a small organization has many pressing concerns and the software choices you make may differ from those Google made, it’s still worth putting lightweight reliability support in place early on, because it’s less costly to expand a structure later on than it is to introduce one that is not present. Part IV contains a number of best practices for training, communication, and meetings that we’ve found to work well for us, many of which should be immediately usable by your organization.

当然，更多以可靠性为导向的软件和系统工程本质上是好的。然而，我们承认，较小的组织可能会想知道如何最好地利用这里代表的经验：就像安全性一样，越早关注可靠性越好。这意味着，即使小型组织有许多紧迫的问题，您所做的软件选择可能与Google所做的不同，但仍值得在早期构建轻量级的可靠性支持，因为后来扩展结构的成本要比引入不存在的结构的成本低。第四部分包含了我们发现对我们有效的一些培训、沟通和会议的最佳实践，其中许多应该能够立即为您的组织所用。

But for sizes between a startup and a multinational, there probably already is someone in your organization who is doing SRE work, without it necessarily being called that name, or recognized as such. Another way to get started on the path to improving reliability for your organization is to formally recognize that work, or to find these people and foster what they do—reward it. They are people who stand on the cusp between one way of looking at the world and another one: like Newton, who is sometimes called not the world’s first physicist, but the world’s last alchemist.

但是对于处于初创企业和跨国公司之间的规模，可能已经有人在您的组织中进行SRE工作，而不一定被称为这个名字，或被认可为这样的工作。开始为组织改进可靠性的另一种方法是正式承认这项工作，或者找到这些人并培养他们所做的事情-奖励他们。他们是站在一种看世界的方式和另一种看世界的方式之间的人：就像牛顿一样，有时被称为不是世界上第一个物理学家，而是世界上最后一个炼金术士。

And taking the historical view, who, then, looking back, might be the first SRE?

而从历史的角度来看，谁可能是第一个SRE？

We like to think that Margaret Hamilton, working on the Apollo program on loan from MIT, had all of the significant traits of the first SRE.5 In her own words, “part of the culture was to learn from everyone and everything, including from that which one would least expect.”

我们认为Margaret Hamilton在阿波罗计划中的工作就具备了第一个SRE的所有重要特质。她自己说：“文化的一部分是向每个人和每件事学习，包括从最意想不到的事物中学习。”

With an SRE’s instincts, Margaret submitted a program change request to add special error checking code in the onboard flight software in case an astronaut should, by accident, happen to select P01 during flight. But this move was considered unnecessary by the “higher-ups” at NASA: of course, that could never happen! So instead of adding error checking code, Margaret updated the mission specifications documentation to say the equivalent of “Do not select P01 during flight.” (Apparently the update was amusing to many on the project, who had been told many times that astronauts would not make any mistakes—after all, they were trained to be perfect.)

出于SRE的直觉，Margaret提交了一个程序更改请求，以添加特殊的错误检查代码到机载飞行软件中，以防万一宇航员在飞行过程中不小心选择了P01。但这一举动被NASA的“高层人士”认为是不必要的：当然，这种情况永远不会发生！所以Margaret更新了任务规格文档，相当于说“不要在飞行过程中选择P01”。（显然，这个更新对许多项目人员来说是滑稽的，因为他们被告知宇航员不会犯任何错误——毕竟他们接受了完美的训练。）

Well, Margaret’s suggested safeguard was only considered unnecessary until the very next mission, on Apollo 8, just days after the specifications update. During midcourse on the fourth day of flight with the astronauts Jim Lovell, William Anders, and Frank Borman on board, Jim Lovell selected P01 by mistake—as it happens, on Christmas Day—creating much havoc for all involved. This was a critical problem, because in the absence of a workaround, no navigation data meant the astronauts were never coming home. Thankfully, the documentation update had explicitly called this possibility out, and was invaluable in figuring out how to upload usable data and recover the mission, with not much time to spare.

Margaret提出的安全保障措施，直到下一次任务才被认为是不必要的，即阿波罗8号任务。该任务在规格更新后的几天内启动，当时宇航员Jim Lovell不小心选择了P01（恰好在圣诞节），导致所有人都陷入了混乱。这是一个严重的问题，因为在没有解决方法的情况下，没有导航数据就意味着宇航员再也回不来了。谢天谢地，文档更新已经明确指出了这种可能性，并且在有限的时间内有助于上传可用数据并恢复任务。

As Margaret says, “a thorough understanding of how to operate the systems was not enough to prevent human errors,” and the change request to add error detection and recovery software to the prelaunch program P01 was approved shortly afterwards.

正如Margaret所说，“对系统如何运作的彻底理解并不足以防止人为错误”，不久之后，添加错误检测和恢复软件到预启动程序P01的变更请求得到了批准。

Although the Apollo 8 incident occurred decades ago, there is much in the preceding paragraphs directly relevant to engineers’ lives today, and much that will continue to be directly relevant in the future. Accordingly, for the systems you look after, for the groups you work in, or for the organizations you’re building, please bear the SRE Way in mind: thoroughness and dedication, belief in the value of preparation and documentation, and an awareness of what could go wrong, coupled with a strong desire to prevent it. Welcome to our emerging profession!

虽然阿波罗8号事件发生在几十年前，但前面的段落中有许多直接关系到工程师今天的生活，而且将来也将继续直接相关。因此，对于您所负责的系统、您所在的团队或您正在建设的组织，请牢记SRE的方式：彻底和投入、相信准备和文档的价值，意识到可能发生的问题，并强烈希望防止它。欢迎来到我们新兴的职业！
