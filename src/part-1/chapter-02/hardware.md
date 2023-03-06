## **Hardware**

## **硬件**

Most of Google’s compute resources are in Google-designed datacenters with propri‐ etary power distribution, cooling, networking, and compute hardware (see [Bar13]). Unlike “standard” colocation datacenters, the compute hardware in a Google- designed datacenter is the same across the board.1 To eliminate the confusion between server hardware and server software, we use the following terminology throughout the book:

* Machine：A piece of hardware (or perhaps a VM)
* Server：A piece of software that implements a service

Machines can run any server, so we don’t dedicate specific machines to specific server programs. There’s no specific machine that runs our mail server, for example. Instead, resource allocation is handled by our cluster operating system, Borg.

We realize this use of the word server is unusual. The common use of the word con‐ flates “binary that accepts network connection” with machine, but differentiating between the two is important when talking about computing at Google. Once you get used to our usage of server, it becomes more apparent why it makes sense to use this specialized terminology, not just within Google but also in the rest of this book.

Figure 2-1 illustrates the topology of a Google datacenter:

* Tens of machines are placed in a rack.
* Racks stand in a row.
* One or more rows form a cluster.
* Usually a datacenter building houses multiple clusters.
* Multiple datacenter buildings that are located close together form a campus.

![[Figure 2-1. Example Google datacenter campus topology]](./figures/2-1.png)

<br>

---

**[Back to contents of the chapter（返回章节目录）](the_production_environment_at_google_from_the_viewpoint_of_an_sre.md)**

* **Next Section（下一节）：[Google’s Approach to Service Management:Site Reliability Engineering（谷歌的服务管理方法：SRE）](google's_approach_to_service_management_site_reliability_engineering.md)**
