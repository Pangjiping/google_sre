## **Our Software Infrastructure**

## **软件基础设施**

Our software architecture is designed to make the most efficient use of our hardware infrastructure. Our code is heavily multithreaded, so one task can easily use many cores. To facilitate dashboards, monitoring, and debugging, every server has an HTTP server that provides diagnostics and statistics for a given task.

我们的软件架构旨在最大限度地利用我们的硬件基础设施。我们的代码具有很强的多线程性，因此一个任务可以轻松地使用多个核心。为了便于仪表板、监视和调试，每个服务器都有一个HTTP服务器，为给定任务提供诊断和统计信息。

All of Google’s services communicate using a Remote Procedure Call (RPC) infrastructure named Stubby; an open source version, gRPC, is available. Often, an RPC call is made even when a call to a subroutine in the local program needs to be performed. This makes it easier to refactor the call into a different server if more modularity is needed, or when a server’s codebase grows. GSLB can load balance RPCs in the same way it load balances externally visible services.

所有谷歌的服务都使用名为Stubby的RPC基础架构进行通信；gRPC是其开源版本。即使需要调用本地程序的子例程，也通常会进行RPC调用。这使得在需要更多模块化或服务器代码库增长时，更容易将调用重构到不同的服务器中。GSLB可以像均衡外部可见服务一样均衡RPC。

A server receives RPC requests from its frontend and sends RPCs to its backend. In traditional terms, the frontend is called the client and the backend is called the server.

一台服务器从前端接收RPC请求并向后端发送RPC。传统上，前端被称为客户端，后端被称为服务器。

Data is transferred to and from an RPC using protocol buffers,4 often abbreviated to “protobufs,” which are similar to Apache’s Thrift. Protocol buffers have many advantages over XML for serializing structured data: they are simpler to use, 3 to 10 times smaller, 20 to 100 times faster, and less ambiguous.

数据通过协议缓冲区（protocol buffers）进行RPC请求和响应的传输，常被缩写为“protobufs”，类似于Apache的Thrift。相比于XML序列化结构化数据，协议缓冲区具有许多优点：使用更简单、大小缩小3-10倍、速度提高20-100倍、且不容易出现歧义。

<br>

---

**[Back to contents of the chapter（返回章节目录）](the_production_environment_at_google_from_the_viewpoint_of_an_sre.md)**

* **Previous Section（上一节）：[Other System Software（其他系统软件）](other_system_software.md)**
* **Next Section（下一节）：[Our Development Environment（开发环境）](our_development_env.md)**
