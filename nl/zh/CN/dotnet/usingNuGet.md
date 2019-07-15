---

copyright:
  years: 2015, 2018
lastupdated: "2017-05-31"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 关于定制 NuGet 数据包源
{: #customizing_nuget}
您可以使用应用程序根目录中的 NuGet.Config 文件来控制应用程序在何处下载依赖关系。在以下示例中，配置 `<packageSources>` 属性可以定义应用程序用来检索数据包的任意键和 API URL。
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}
