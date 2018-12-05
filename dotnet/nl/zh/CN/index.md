---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET 核心
{: #dotnet_core}

{{site.data.keyword.Bluemix}} 上的“ASP.NET 核心”运行时采用“ASP.NET 核心”buildpack 技术。“ASP.NET 核心”是用于构建 .NET Web 应用程序的模块化开放式源代码框架。“.Net 核心”是跨平台的小型运行时，可由“ASP.NET 核心”应用程序实现。将它们相结合可实现基于云的先进 Web 应用程序。
{: shortdesc}

## 检测
{: #detection}
如果应用程序中的任何位置存在一个或多个包含 project.json 文件和至少一个 .cs 文件的文件夹，或者应用程序是从 *dotnet publish* 命令的输出目录进行推送，那么将使用 {{site.data.keyword.Bluemix}} 的“ASP.NET 核心”buildpack。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} 提供了“ASP.NET 核心”入门模板应用程序。“ASP.NET 核心”入门模板应用程序是一个简单的应用程序，它提供了一个可供您使用的模板。您可以尝试使用该入门模板应用程序来进行更改并将更改推送到 {{site.data.keyword.Bluemix_notm}} 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](../common/starter_app_usage.html)。
