## **I Won’t Give Up My Code!**

## **我不会放弃我的代码！**

Because engineers are human beings who often form an emotional attachment to their creations, confrontations over large-scale purges of the source tree are not uncommon. Some might protest, "What if we need that code later?" "Why don’t we just comment the code out so we can easily add it again later?" or "Why don’t we gate the code with a flag instead of deleting it?" These are all terrible suggestions. Source control systems make it easy to reverse changes, whereas hundreds of lines of commented code create distractions and confusion (especially as the source files continue to evolve), and code that is never executed, gated by a flag that is always disabled, is a metaphorical time bomb waiting to explode, as painfully experienced by Knight Capital, for example (see "Order In the Matter of Knight Capital Americas LLC" [Sec13]).

因为工程师是经常对他们的创作产生情感依恋的人，所以反对源代码大规模清除并不少见。有些人可能会抗议，“如果我们以后需要那个代码怎么办？”，“为什么我们不把代码注释掉，这样我们以后就可以很容易地再次添加它了？”或“为什么我们不用标志位来控制代码而不是删除它？”这些都是糟糕的建议。源代码控制系统使撤销更改变得容易，而数百行注释代码会造成干扰和混乱（尤其是当源文件不断发展时）。永远不会执行的代码由始终禁用的标志门控，是一个等待爆炸的定时炸弹。例如Knight Capital的痛苦经历（请参阅“Order In the Matter of Knight Capital Americas LLC”[Sec13]）。

At the risk of sounding extreme, when you consider a web service that’s expected to be available 24/7, to some extent, every new line of code written is a liability. SRE promotes practices that make it more likely that all code has an essential purpose, such as scrutinizing code to make sure that it actually drives business goals, routinely removing dead code, and building bloat detection into all levels of testing.

冒着极端的风险，当您考虑预计24/7全天候可用的Web服务时，在某种程度上，编写的每一行新代码都是一种责任。SRE提倡使所有代码更有可能具有基本目的的做法，例如审查代码以确保它真正推动业务目标，定期删除无用代码，以及在所有级别的测试中构建膨胀检测。
