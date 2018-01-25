---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 故障诊断 FAQ
{: #troubleshooting_faq}

**问**：我的应用程序无法部署，消息为：`API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  这意味着什么？

**答**：如果在推送应用程序时您收到类似消息，那么很可能是因为应用程序超过内存或磁盘限额限制导致的。通过增加应用程序的配额可以解决此问题。

**问**：我的应用程序无法部署，消息为：`Failed to compress droplet: signal: broken pipe` 或 `No space left on device`。该如何解决这个问题？

**答**：从包含大量 NuGet 数据包依赖项的源代码推送的项目，有时会在启用 NuGet 数据包高速缓存时导致此错误。将 `CACHE_NUGET_PACKAGES` 环境变量设置为 `false` 以禁用高速缓存。请参阅有关如何[禁用 NuGet 数据包](diablingNuGet.md)的指示信息以了解更多信息。

# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET 核心概述](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
