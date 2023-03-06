# **Preface**

# **序言**

Software engineering has this in common with having children: the labor before the birth is painful and difficult, but the labor after the birth is where you actually spend most of your effort. Yet software engineering as a discipline spends much more time talking about the first period as opposed to the second, despite estimates that 40–90% of the total costs of a system are incurred after birth. The popular industry model that conceives of deployed, operational software as being “stabilized” in production, and therefore needing much less attention from software engineers, is wrong. Through this lens, then, we see that if software engineering tends to focus on designing and building software systems, there must be another discipline that focuses on the whole lifecycle of software objects, from inception, through deployment and operation, refinement, and eventual peaceful decommissioning. This discipline uses—and needs to use—a wide range of skills, but has separate concerns from other kinds of engineers. Today, our answer is the discipline Google calls Site Reliability Engineering.

软件工程和生孩子有一个共同点：生产前是痛苦和艰辛的，而生产后才是你真正付出最大努力的地方。然而，软件工程作为一门学科花更多的时间谈论第一个时期而不是第二个时期，尽管据估计系统总成本的40%-90%是在软件诞生后发生的。部署的流行的行业模型，将操作软件视为在生产中变得“稳定”，因此需要软件工程师的更少的关注，这是错误的。然后，通过这个镜头，我们看到如果软件工程倾向于专注于设计和构建软件系统，那么必须有另一门学科专注于软件对象的整个生命周期，从开始，到部署和操作，再到改进，并最终平滑退役。该学科使用——并且需要使用——范围广泛的技能，但与其他类型的工程师有着不同的关注点。今天，我们的答案是Google称之为站点可靠性工程(SRE)的学科。

So what exactly is Site Reliability Engineering (SRE)? We admit that it’s not a particularly clear name for what we do—pretty much every site reliability engineer at Google gets asked what exactly that is, and what they actually do, on a regular basis.

那么站点可靠性工程(SRE)到底是什么？我们承认，对于我们所做的事情来说，这并不是一个特别明确的名称——几乎Google的每一位站点可靠性工程师都会定期被问到这到底是什么，以及他们实际做了什么。

Unpacking the term a little, first and foremost, SREs are engineers. We apply the principles of computer science and engineering to the design and development of computing systems: generally, large distributed ones. Sometimes, our task is writing the software for those systems alongside our product development counterparts; sometimes, our task is building all the additional pieces those systems need, like backups or load balancing, ideally so they can be reused across systems; and sometimes, our task is figuring out how to apply existing solutions to new problems.

稍微解释一下这个术语，首先，SRE是工程师。我们将计算机科学和工程原理应用于计算系统的设计和开发：通常是大型分布式系统。有时，我们的任务是与我们的产品开发同事一起为这些系统编写软件；有时，我们的任务是构建这些系统所需的所有附加部分，如备份或负载均衡，理想情况下它们可以跨系统重用；有时，我们的任务是弄清楚如何将现有解决方案应用于新问题。

Next, we focus on system reliability. Ben Treynor Sloss, Google’s VP for 24/7 Operations, originator of the term SRE, claims that reliability is the most fundamental feature of any product: a system isn’t very useful if nobody can use it! Because reliability2 is so critical, SREs are focused on finding ways to improve the design and operation of systems to make them more scalable, more reliable, and more efficient. However, we expend effort in this direction only up to a point: when systems are “reliable enough,” we instead invest our efforts in adding features or building new products.

接下来，我们关注系统可靠性。Ben Treynor Sloss，Google的24/7运营副总裁，术语SRE的创始人，声称可靠性是任何产品最基本的特性：如果没有人可以使用，系统就不是很有用！由于可靠性非常重要，因此SRE专注于寻找改进系统设计和操作的方法，以使其更具可扩展性、更可靠和更高效。然而，我们在这个方向上的努力只为了达到了一个目标：当系统“足够可靠”时，我们可以会投入精力添加功能或构建新产品。

Finally, SREs are focused on operating services built atop our distributed computing systems, whether those services are planet-scale storage, email for hundreds of millions of users, or where Google began, web search. The “site” in our name originally referred to SRE’s role in keeping the google.com website running, though we now run many more services, many of which aren’t themselves websites—from internal infrastructure such as Bigtable to products for external developers such as the Google Cloud Platform.

最后，SRE专注于在我们的分布式计算系统之上构建的运营服务，无论这些服务是全球规模的存储、数亿用户的电子邮件，还是谷歌的网络搜索。我们名称中的“站点”最初指的是SRE在保持google.com网站运行方面的作用，尽管我们现在运行了更多的服务，其中许多本身并不是网站——从Bigtable等内部基础设施到外部产品开发人员，例如Google Cloud Platform。

Although we have represented SRE as a broad discipline, it is no surprise that it arose in the fast-moving world of web services, and perhaps in origin owes something to the peculiarities of our infrastructure. It is equally no surprise that of all the postdeployment characteristics of software that we could choose to devote special attention to, reliability is the one we regard as primary. The domain of web services, both because the process of improving and changing server-side software is comparatively contained, and because managing change itself is so tightly coupled with failures of all kinds, is a natural platform from which our approach might emerge.

尽管我们将SRE描述为一门广泛的学科，但它出现在快速发展的Web服务世界中并不足为奇，也许起源于我们基础设施的特殊性。同样不足为奇的是，在我们可以选择特别关注的软件的所有部署后特征中，可靠性是我们认为最重要的特征。Web服务领域，既因为改进和更改服务器端软件的过程相对包含，也因为管理更改本身与各种故障紧密相关，因此是我们的方法可能出现的自然平台。

Despite arising at Google, and in the web community more generally, we think that this discipline has lessons applicable to other communities and other organizations. This book is an attempt to explain how we do things: both so that other organizations might make use of what we’ve learned, and so that we can better define the role and what the term means. To that end, we have organized the book so that general principles and more specific practices are separated where possible, and where it’s appropriate to discuss a particular topic with Google-specific information, we trust that the reader will indulge us in this and will not be afraid to draw useful conclusions about their own environment.

尽管出现在Google以及更普遍的网络社区中，我们认为该学科具有适用于其他社区和其他组织的经验教训。这本书试图解释我们是如何做事的：既让其他组织可以利用我们学到的东西，也让我们可以更好地定义角色和术语的含义。为此，我们对本书进行了组织，以便在可能的情况下将一般原则和更具体的实践分开，并且在适当的地方讨论特定主题与Google特定信息，我们相信读者会沉迷于这本书，并且不会害怕对自己的环境得出有用的结论。

We have also provided some orienting material—a description of Google’s production environment and a mapping between some of our internal software and publicly available software—which should help to contextualize what we are saying and make it more directly usable.

我们还提供了一些指导材料——对Google生产环境的描述以及我们的一些内部软件和公开可用软件之间的映射——这应该有助于将我们所说的内容联系起来，并使其更直接可用。

Ultimately, of course, more reliability-oriented software and systems engineering is inherently good. However, we acknowledge that smaller organizations may be wondering how they can best use the experience represented here: much like security, the earlier you care about reliability, the better. This implies that even though a small organization has many pressing concerns and the software choices you make may differ from those Google made, it’s still worth putting lightweight reliability support in place early on, because it’s less costly to expand a structure later on than it is to introduce one that is not present. Part IV contains a number of best practices for training, communication, and meetings that we’ve found to work well for us, many of which should be immediately usable by your organization.

当然，更多面向可靠性的软件和系统工程本质上是好的。然而，我们承认，较小的组织可能想知道他们如何才能最好地利用这里所展示的经验：就像安全一样，你越早关心可靠性越好。这意味着即使小型组织有许多紧迫的问题并且您做出的软件选择可能与Google做出的选择不同，但仍然值得尽早提供轻量级可靠性支持，因为以后扩展结构的成本低于现在引入一个不存在的。第IV部分包含一些我们发现对我们很有效的培训、沟通和会议最佳实践，其中许多应该可以立即被您的组织使用。

But for sizes between a startup and a multinational, there probably already is someone in your organization who is doing SRE work, without it necessarily being called that name, or recognized as such. Another way to get started on the path to improving reliability for your organization is to formally recognize that work, or to find these people and foster what they do—reward it. They are people who stand on the cusp between one way of looking at the world and another one: like Newton, who is sometimes called not the world’s first physicist, but the world’s last alchemist.

但是对于介于初创公司和跨国公司之间的规模，您的组织中可能已经有人在从事SRE工作，但不一定被称为那个名字，或被认可。开始提高组织可靠性的另一种方法是正式认可这项工作，或者找到这些人并培养他们所做的事情——奖励。他们是站在一种看待世界的方式和另一种看待世界的方式之间的风口浪尖上的人：就像牛顿，有时人们称他不是世界上第一位物理学家，而是世界上最后的炼金术士。

And taking the historical view, who, then, looking back, might be the first SRE?

而从历史的角度来看，谁可能是第一个SRE？

We like to think that Margaret Hamilton, working on the Apollo program on loan from MIT, had all of the significant traits of the first SRE.5 In her own words, “part of the culture was to learn from everyone and everything, including from that which one would least expect.”

我们倾向于认为从麻省理工学院借调从事阿波罗计划工作的Margaret Hamilton具有第一个SRE的所有重要特征。用她自己的话说，“文化的一部分是向每一个人和每一件事学习，包括向人们最意想不到的事情学习。”

With an SRE’s instincts, Margaret submitted a program change request to add special error checking code in the onboard flight software in case an astronaut should, by accident, happen to select P01 during flight. But this move was considered unnecessary by the “higher-ups” at NASA: of course, that could never happen! So instead of adding error checking code, Margaret updated the mission specifications documentation to say the equivalent of “Do not select P01 during flight.” (Apparently the update was amusing to many on the project, who had been told many times that astronauts would not make any mistakes—after all, they were trained to be perfect.)

出于SRE的直觉，Margaret提交了一项程序更改请求，以在机载飞行软件中添加特殊的错误检查代码，防止宇航员在飞行过程中意外选择P01。但是这个举动被NASA的“高层”认为是不必要的：当然，那永远不可能发生！因此，Margaret没有添加错误检查代码，而是更新了任务规范文档，“飞行期间不要选择P01”。（显然，这个更新对项目中的许多人来说很有趣，他们曾多次被告知宇航员不会犯任何错误——毕竟，他们受过完美训练。）

Well, Margaret’s suggested safeguard was only considered unnecessary until the very next mission, on Apollo 8, just days after the specifications update. During midcourse on the fourth day of flight with the astronauts Jim Lovell, William Anders, and Frank Borman on board, Jim Lovell selected P01 by mistake—as it happens, on Christmas Day—creating much havoc for all involved. This was a critical problem, because in the absence of a workaround, no navigation data meant the astronauts were never coming home. Thankfully, the documentation update had explicitly called this possibility out, and was invaluable in figuring out how to upload usable data and recover the mission, with not much time to spare.

好吧，Margaret建议的保障措施直到下一次阿波罗8号任务才被认为是不必要的，就在规范更新几天后。在宇航员 Jim Lovell、William Anders和Frank Borman登机的第四天飞行中途，Jim Lovell错误地选择了P01——碰巧发生在圣诞节——给所有相关人员造成了很大的破坏。这是一个关键问题，因为在没有解决方法的情况下，没有导航数据意味着宇航员永远无法回家。值得庆幸的是，文档更新已经明确排除了这种可能性，并且在弄清楚如何上传可用数据和恢复任务方面非常宝贵，没有太多时间可以空闲。

As Margaret says, “a thorough understanding of how to operate the systems was not enough to prevent human errors,” and the change request to add error detection and recovery software to the prelaunch program P01 was approved shortly afterwards.

正如Margaret所说，“对如何操作系统的透彻理解不足以防止人为错误”。不久之后，将错误检测和恢复软件添加到预启动程序P01的变更请求获得批准。

Although the Apollo 8 incident occurred decades ago, there is much in the preceding paragraphs directly relevant to engineers’ lives today, and much that will continue to be directly relevant in the future. Accordingly, for the systems you look after, for the groups you work in, or for the organizations you’re building, please bear the SRE Way in mind: thoroughness and dedication, belief in the value of preparation and documentation, and an awareness of what could go wrong, coupled with a strong desire to prevent it. Welcome to our emerging profession!

尽管阿波罗8号事件发生在几十年前，但前面的段落中有很多内容与当今工程师的生活直接相关，而且很多内容将在未来继续直接相关。因此，对于您管理的系统、您工作的团队或您正在建立的组织，请牢记SRE方式：彻底和奉献精神，对准备和文档价值的信念，对可能出问题的意识，以及防止它发生的强烈愿望。欢迎来到我们的新兴职业！
