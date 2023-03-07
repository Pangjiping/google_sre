# **Foreword**

# **前言**

> — Mark Burgess
>
> author of In Search of Certainty
>
> Oslo, March 2016

Google’s story is a story of scaling up. It is one of the great success stories of the computing industry, marking a shift towards IT-centric business. Google was one of the first companies to define what business-IT alignment meant in practice, and went on to inform the concept of DevOps for a wider IT community. This book has been writ‐ ten by a broad cross-section of the very people who made that transition a reality.

谷歌的故事是一个关于扩展的故事。它是计算机行业的伟大成功故事之一，标志着向以IT为中心的业务的转变。谷歌是最早定义实践中什么是业务-IT对齐的公司之一，并继续向更广泛的IT社区传递DevOps的概念。本书由那些使这一转变成为现实的广泛的人群撰写。

Google grew at a time when the traditional role of the system administrator was being transformed. It questioned system administration, as if to say: we can’t afford to hold tradition as an authority, we have to think anew, and we don’t have time to wait for everyone else to catch up. In the introduction to Principles of Network and System Administration [[Bur99]](https://www.wiley.com/en-us/Principles+of+Network+and+System+Administration%2C+2nd+Edition-p-9780470868072), I claimed that system administration was a form of humancomputer engineering. This was strongly rejected by some reviewers, who said “we are not yet at the stage where we can call it engineering.” At the time, I felt that the field had become lost, trapped in its own wizard culture, and could not see a way forward. Then, Google drew a line in the silicon, forcing that fate into being. The revised role was called SRE, or Site Reliability Engineer. Some of my friends were among the first of this new generation of engineer; they formalized it using software and automation. Initially, they were fiercely secretive, and what happened inside and outside of Google was very different: Google’s experience was unique. Over time, information and methods have flowed in both directions. This book shows a willingness to let SRE thinking come out of the shadows.

Google在传统系统管理员的角色正在被转变的时候开始快速发展。它质疑了系统管理，好像在说：我们不能把传统当作权威，我们必须重新思考，我们没有时间等待其他人跟上。在《网络和系统管理原理》（Principles of Network and System Administration）[[Bur99]](https://www.wiley.com/en-us/Principles+of+Network+and+System+Administration%2C+2nd+Edition-p-9780470868072)的介绍中，我声称系统管理是一种人机工程学。这受到了一些审稿人的强烈反对，他们说“我们还没有达到可以称之为工程的阶段”。当时，我觉得这个领域已经迷失了方向，陷入了自己的巫师文化中，无法找到前进的道路。然后，谷歌在硅片上划了一条线，强迫这个命运成为现实。新的角色被称为SRE，即现场可靠性工程师。我的一些朋友是这个新一代工程师中的第一批；他们使用软件和自动化来规范化它。起初，他们非常保密，谷歌内外发生的事情有很大不同：谷歌的经验是独一无二的。随着时间的推移，信息和方法在两个方向上都流动。这本书表明了一种愿望，即让SRE思想走出阴影。

Here, we see not only how Google built its legendary infrastructure, but also how it studied, learned, and changed its mind about the tools and the technologies along the way. We, too, can face up to daunting challenges with an open spirit. The tribal nature of IT culture often entrenches practitioners in dogmatic positions that hold the industry back. If Google overcame this inertia, so can we.

在这里，我们不仅可以看到 Google 是如何构建其传奇基础架构的，还可以看到它是如何研究、学习并改变对工具和技术的看法的。我们也可以以开放的精神迎接令人生畏的挑战。IT 文化的部落性质经常使从业者陷入教条主义的立场，这阻碍了行业的发展。如果 Google 能够克服这种惯性，我们也可以。

This book is a collection of essays by one company, with a single common vision. The fact that the contributions are aligned around a single company’s goal is what makes it special. There are common themes, and common characters (software systems) that reappear in several chapters. We see choices from different perspectives, and know that they correlate to resolve competing interests. The articles are not rigorous, academic pieces; they are personal accounts, written with pride, in a variety of personal styles, and from the perspective of individual skill sets. They are written bravely, and with an intellectual honesty that is refreshing and uncommon in industry literature. Some claim “never do this, always do that,” others are more philosophical and tentative, reflecting the variety of personalities within an IT culture, and how that too plays a role in the story. We, in turn, read them with the humility of observers who were not part of the journey, and do not have all the information about the myriad conflicting challenges. Our many questions are the real legacy of the volume: Why didn’t they do X? What if they’d done Y? How will we look back on this in years to come? It is by comparing our own ideas to the reasoning here that we can measure our own thoughts and experiences.

本书是一家公司的文章集，具有共同的愿景。这些文章围绕着一家公司的目标，具有共同的主题和出现在几个章节中的共同角色（软件系统）。我们从不同的角度看到了决策，并了解它们如何协调解决竞争利益。这些文章不是严谨的学术文章；它们是个人带着骄傲写成的，用各种个人风格写成的，从个人技能集的角度来看待问题。它们写得勇敢，具有一种令人耳目一新、在业界文献中不常见的思想诚实。有些人声称“永远不要这样做，总是要这样做”，而其他人则更具哲学性和暂定性，反映了IT文化中的个性多样性，以及这也在故事中发挥了作用。相比之下，我们以观察者的谦卑姿态阅读这些文章，没有参与旅程，也没有所有关于无数相互矛盾的挑战的信息。我们的许多问题是这本书的真正财富：他们为什么不做X？如果他们做了Y会怎样？多年后我们会如何回顾这个问题？通过将我们自己的想法与这里的推理进行比较，我们可以衡量自己的思想和经验。

The most impressive thing of all about this book is its very existence. Today, we hear a brazen culture of “just show me the code.” A culture of “ask no questions” has grown up around open source, where community rather than expertise is championed. Google is a company that dared to think about the problems from first principles, and to employ top talent with a high proportion of PhDs. Tools were only components in processes, working alongside chains of software, people, and data. Nothing here tells us how to solve problems universally, but that is the point. Stories like these are far more valuable than the code or designs they resulted in. Implementations are ephemeral, but the documented reasoning is priceless. Rarely do we have access to this kind of insight.

这本书最令人印象深刻的事情是它的存在。如今，我们听到了一种“只展示代码”的大胆文化。在开源社区中，出现了一种“不要问问题”的文化，社区而不是专业技术被推崇。Google是一家敢于从第一原理考虑问题，并雇用高比例博士学位人才的公司。工具只是流程中的组件，与软件、人员和数据链条一起工作。这里没有告诉我们如何普遍解决问题，但这就是重点。这样的故事比它们所产生的代码或设计更有价值。实现是短暂的，但记录下的推理是无价的。我们很少有机会接触到这种洞察力。

This, then, is the story of how one company did it. The fact that it is many overlapping stories shows us that scaling is far more than just a photographic enlargement of a textbook computer architecture. It is about scaling a business process, rather than just the machinery. This lesson alone is worth its weight in electronic paper.

这就是一个公司是如何实现这件事的故事。事实上，由于它涉及到许多重叠的故事，这表明扩展远不仅仅是对教科书计算机架构的照片式放大。它关于扩展业务流程，而不仅仅是机械的扩展。这个教训本身就是值得记录。

We do not engage much in self-critical review in the IT world; as such, there is much reinvention and repetition. For many years, there was only the USENIX LISA conference community discussing IT infrastructure, plus a few conferences about operating systems. It is very different today, yet this book still feels like a rare offering: a detailed documentation of Google’s step through a watershed epoch. The tale is not for copying—though perhaps for emulating—but it can inspire the next step for all of us. There is a unique intellectual honesty in these pages, expressing both leadership and humility. These are stories of hopes, fears, successes, and failures. I salute the courage of authors and editors in allowing such candor, so that we, who are not party to the hands-on experiences, can also benefit from the lessons learned inside the cocoon.

在IT领域，我们很少进行自我批评；因此，会有很多重新发明和重复。多年来，只有USENIX LISA会议社区讨论IT基础设施，还有一些关于操作系统的会议。今天已经非常不同了，但这本书仍然感觉像是一份珍贵的馈赠：详细记录了谷歌经历历史性时期的步伐。这个故事并不是要被复制的——尽管也许可以效仿——但它可以激发我们所有人迈出下一步的勇气。这些文章表现了独特的知识诚实，表达了领导力和谦卑。这些是希望、恐惧、成功和失败的故事。我向作者和编辑的勇气致敬，他们允许如此坦率地表达，以便我们这些没有亲身经历的人也能从中学到经验教训。
