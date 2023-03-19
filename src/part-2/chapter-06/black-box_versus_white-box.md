## **Black-Box Versus White-Box**

## **黑盒与白盒**

We combine heavy use of white-box monitoring with modest but critical uses of black-box monitoring. The simplest way to think about black-box monitoring versus white-box monitoring is that black-box monitoring is symptom-oriented and represents active—not predicted—problems: "The system isn’t working correctly, right now." White-box monitoring depends on the ability to inspect the innards of the system, such as logs or HTTP endpoints, with instrumentation. White-box monitoring therefore allows detection of imminent problems, failures masked by retries, and so forth.

我们将大量使用白盒监控与适度但关键的黑盒监控相结合。思考黑盒监控与白盒监控的最简单方式是，黑盒监控是面向症状的，代表主动的而不是预测的问题。“系统现在不能正常工作”。白盒监控取决于用仪器检查系统内部的能力，如日志或HTTP端点。因此，白盒监控允许检测即将发生的问题，以及被重试掩盖的故障，等等。

Note that in a multilayered system, one person’s symptom is another person’s cause. For example, suppose that a database’s performance is slow. Slow database reads are a symptom for the database SRE who detects them. However, for the frontend SRE observing a slow website, the same slow database reads are a cause. Therefore, white- box monitoring is sometimes symptom-oriented, and sometimes cause-oriented, depending on just how informative your white-box is.

请注意，在一个多层次的系统中，一个系统的问题就是另一个系统的原因。例如，假设一个数据库的性能很慢。对于数据库SRE来说，缓慢的数据库读取是一个问题，他检测到了这些问题。然而，对于观察缓慢网站的前端SRE来说，同样缓慢的数据库读取是一个原因。因此，白盒监控有时是面向问题的，有时是面向原因的，这取决于你的白盒的信息量有多大。

When collecting telemetry for debugging, white-box monitoring is essential. If web servers seem slow on database-heavy requests, you need to know both how fast the web server perceives the database to be, and how fast the database believes itself to be. Otherwise, you can’t distinguish an actually slow database server from a network problem between your web server and your database.

在收集用于调试的数据时，白盒监控是必不可少的。如果网络服务器在数据库的大量请求中显得很慢，你需要知道网络服务器认为数据库有多快，以及数据库认为自己有多快。否则，你就无法区分数据库服务器的实际速度与Web服务器和数据库之间的网络问题。

For paging, black-box monitoring has the key benefit of forcing discipline to only nag a human when a problem is both already ongoing and contributing to real symptoms. On the other hand, for not-yet-occurring but imminent problems, black-box monitoring is fairly useless.

对于呼叫来说，黑盒监控的主要好处是迫使纪律部门只在问题已经发生并导致真正的问题时才对人进行呼叫。另一方面，对于尚未发生但即将发生的问题，黑盒监控是相当无用的。
