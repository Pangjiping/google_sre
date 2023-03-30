## **The Virtue of Boring**

## **无聊的美德**

Unlike just about everything else in life, "boring" is actually a positive attribute when it comes to software! We don’t want our programs to be spontaneous and interesting; we want them to stick to the script and predictably accomplish their business goals. In the words of Google engineer Robert Muth, "Unlike a detective story, the lack of excitement, suspense, and puzzles is actually a desirable property of source code." Surprises in production are the nemeses of SRE.

与生活中的其他一切不同，“无聊”实际上是软件的积极属性！我们不希望程序是自发的和有趣的；我们希望它们遵守脚本并按预期实现业务目标。用Google工程师Robert Muth的话来说，“与侦探故事不同，缺乏刺激、悬念和谜题实际上是源代码的一个可取属性”。生产中的意外是SRE的克星。

As Fred Brooks suggests in his "No Silver Bullet" essay [Bro95], it is very important to consider the difference between essential complexity and accidental complexity. Essential complexity is the complexity inherent in a given situation that cannot be removed from a problem definition, whereas accidental complexity is more fluid and can be resolved with engineering effort. For example, writing a web server entails dealing with the essential complexity of serving web pages quickly. However, if we write a web server in Java, we may introduce accidental complexity when trying to minimize the performance impact of garbage collection.

正如Fred Brooks在他的“No Silver Bullet”文章[Bro95]中建议的那样，考虑基本复杂性和偶然复杂性之间的区别非常重要。基本复杂性是给定情况中固有的复杂性，不能从问题定义中删除，而偶然复杂性则更具流动性，可以通过工程努力解决。例如，编写Web服务器需要处理快速提供网页的基本复杂性。但是，如果我们用Java编写Web服务器，我们可能会在试图最小化垃圾收集对性能的影响时引入意外的复杂性。

With an eye towards minimizing accidental complexity, SRE teams should:

* Push back when accidental complexity is introduced into the systems for which they are responsible
* Constantly strive to eliminate complexity in systems they onboard and for which they assume operational responsibility

为了最大限度地减少偶然复杂性，SRE团队应该：

* 在他们负责的系统中引入意外的复杂性时予以抵制
* 不断努力消除他们所采用的系统的复杂性，并为此承担运维责任
