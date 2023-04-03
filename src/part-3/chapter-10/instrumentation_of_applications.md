## **Instrumentation of Applications**

## **应用程序检测**

The `/varz` HTTP handler simply lists all the exported variables in plain text, as space- separated keys and values, one per line. A later extension added a mapped variable, which allows the exporter to define several labels on a variable name, and then export a table of values or a histogram. An example map-valued variable looks like the following, showing 25 HTTP 200 responses and 12 HTTP 500s:

`/varz`HTTP处理程序简单地以纯文本形式列出所有导出的变量，作为空格分隔的键和值，每行一个。后来的扩展添加了一个映射变量，它允许导出器在变量名称上定义多个标签，然后导出值表或直方图。示例映射值变量如下所示，显示25个HTTP 200响应和12个HTTP 500：

`http_responses map:code 200:25 404:0 500:12`

Adding a metric to a program only requires a single declaration in the code where the metric is needed.

将度量添加到程序只需要在需要度量的代码中进行单个声明。

In hindsight, it’s apparent that this schemaless textual interface makes the barrier to adding new instrumentation very low, which is a positive for both the software engineering and SRE teams. However, this has a trade-off against ongoing maintenance; the decoupling of the variable definition from its use in Borgmon rules requires careful change management. In practice, this trade-off has been satisfactory because tools to validate and generate rules have been written as well.

事后看来，很明显，这种无模式的文本界面使得添加新工具的障碍非常低，这对软件工程和SRE团队都是积极的。但是，这与持续维护有一个权衡；将变量定义与其在Borgmon规则中的使用分离需要谨慎的变更管理。在实践中，这种折衷是令人满意的，因为验证和生成规则的工具也已编写。
