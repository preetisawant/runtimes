---

copyright:
  years: 2015, 2018
lastupdated: "2017-05-31"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 關於自訂 NuGet 套件來源
{: #customizing_nuget}
您可以使用應用程式根目錄中的 NuGet.Config 檔案，控制應用程式下載相依關係的位置。在下列範例中，配置 `<packageSources>` 內容會定義應用程式擷取套件用的任何金鑰和 API URL。
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}
