## **Release Simplicity**

## **发布简洁性**

Simple releases are generally better than complicated releases. It is much easier to measure and understand the impact of a single change rather than a batch of changes released simultaneously. If we release 100 unrelated changes to a system at the same time and performance gets worse, understanding which changes impacted performance, and how they did so, will take considerable effort or additional instrumentation. If the release is performed in smaller batches, we can move faster with more confidence because each code change can be understood in isolation in the larger system. This approach to releases can be compared to gradient descent in machine learning, in which we find an optimum solution by taking small steps at a time, and considering if each change results in an improvement or degradation.

简单版本通常优于复杂版本。**衡量和理解单个更改的影响比同时发布的一批更改要容易得多**。如果我们同时向系统发布100个不相关的更改并且性能变差，了解哪些更改影响了性能以及它们是如何影响的，将需要相当大的努力。如果以较小的批次执行发布，我们可以更有信心地更快地发布，因为每个代码更改都可以在较大的系统中单独理解。这种发布方法可以与机器学习中的梯度下降进行比较，在这种方法中，我们通过一次一小步地找到最佳解决方案，并考虑每个变化是否会导致改进或退化。
