## **The Virtue of Boring**

Unlike just about everything else in life, "boring" is actually a positive attribute when it comes to software! We don’t want our programs to be spontaneous and interesting; we want them to stick to the script and predictably accomplish their business goals. In the words of Google engineer Robert Muth, "Unlike a detective story, the lack of excitement, suspense, and puzzles is actually a desirable property of source code." Surprises in production are the nemeses of SRE.

As Fred Brooks suggests in his "No Silver Bullet" essay [Bro95], it is very important to consider the difference between essential complexity and accidental complexity. Essential complexity is the complexity inherent in a given situation that cannot be removed from a problem definition, whereas accidental complexity is more fluid and can be resolved with engineering effort. For example, writing a web server entails dealing with the essential complexity of serving web pages quickly. However, if we write a web server in Java, we may introduce accidental complexity when trying to minimize the performance impact of garbage collection.

With an eye towards minimizing accidental complexity, SRE teams should:

* Push back when accidental complexity is introduced into the systems for which they are responsible
* Constantly strive to eliminate complexity in systems they onboard and for which they assume operational responsibility
