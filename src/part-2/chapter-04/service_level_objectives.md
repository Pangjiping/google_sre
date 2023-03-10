# **Service Level Objectives**

# **服务水平目标**

> Written by Chris Jones, John Wilkes, and Niall Murphy with Cody Smith
>
> Edited by Betsy Beyer

It’s impossible to manage a service correctly, let alone well, without understanding which behaviors really matter for that service and how to measure and evaluate those behaviors. To this end, we would like to define and deliver a given level of service to our users, whether they use an internal API or a public product.

如果不了解哪些行为对该服务真正重要，以及如何衡量和评估这些行为，就不可能正确地管理一项服务，更不用说做好。为此，我们希望定义并向我们的用户提供特定水平的服务，无论他们使用的是内部API还是公共产品。

We use intuition, experience, and an understanding of what users want to define ser‐ vice level indicators (SLIs), objectives (SLOs), and agreements (SLAs). These measure‐ ments describe basic properties of metrics that matter, what values we want those metrics to have, and how we’ll react if we can’t provide the expected service. Ulti‐ mately, choosing appropriate metrics helps to drive the right action if something goes wrong, and also gives an SRE team confidence that a service is healthy.

我们利用直觉、经验和对用户需求的理解来定义服务水平指标（SLI）、目标（SLO）和协议（SLA）。这些衡量标准描述了重要的衡量标准的基本属性，我们希望这些衡量标准具有什么价值，以及如果我们不能提供预期的服务，我们将如何反应。最终，选择适当的度量有助于在出错时采取正确的行动，也让SRE团队对服务的健康发展充满信心。

This chapter describes the framework we use to wrestle with the problems of metric modeling, metric selection, and metric analysis. Much of this explanation would be quite abstract without an example, so we’ll use the Shakespeare service outlined in ["Shakespeare: A Sample Service"](./../../part-1/chapter-02/shakespare_a_simple_service.md) to illustrate our main points.

这一章描述了我们用来解决指标建模、指标选择和质保分析等问题的框架。如果没有一个例子，大部分的解释将是相当抽象的，所以我们将使用“Shakespeare”中概述的Shakespeare服务。["Shakespeare: A Sample Service"](./../../part-1/chapter-02/shakespare_a_simple_service.md)中概述的服务来说明我们的主要观点。

- [Service Level Terminology（服务水平术语）](service_level_terminology.md)
- [Indicators in Practice（实践中的SLI）](indicators_in_practice.md)
- [Objectives in Practice](objectives_in_practice.md)
- [Agreements in Practice](agreements_in_practice.md)
