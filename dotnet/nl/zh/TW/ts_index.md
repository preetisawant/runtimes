---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 疑難排解常見問題 (FAQ)
{: #troubleshooting_faq}

**問**：我的應用程式無法部署，訊息為：`API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`。這表示什麼？

**答**：如果您在推送應用程式時收到類似訊息，最可能是因為應用程式超出記憶體或磁碟限額限制。增加應用程式的配額，即可解決此問題。

**問**：我的應用程式無法部署，訊息為：`Failed to compress droplet: signal: broken pipe` 或 `No space left on device`。如何修正這個問題？

**答**：從包含大量 NuGet 套件相依關係的原始碼中所推送的專案，有時可能會在啟用 NuGet 套件快取時造成此錯誤。將 `CACHE_NUGET_PACKAGES` 環境變數設為 `false`，即可停用快取。如需相關資訊，請參閱有關如何[停用 NuGet 套件](diablingNuGet.md)的指示。

# 相關鏈結
{: #rellinks notoc}
## 一般
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core Overview](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
