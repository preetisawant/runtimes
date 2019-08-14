---

copyright:
  years: 2015, 2018
lastupdated: "2017-05-31"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 定制 NuGet 包源
{: #customizing_nuget}

您可以使用应用程序根目录中的 `NuGet.Config` 文件来控制应用程序在何处下载依赖关系。在以下示例中，通过配置 `<packageSources>` 属性，可以为应用程序定义用来检索包的任何密钥和 API URL。
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}
