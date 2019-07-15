---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 本地运行 Node.js 应用程序
{: #hints}

设置用于本地运行 Node.js 应用程序的端口号，避免在 {{site.data.keyword.Bluemix}} 上运行时产生冲突。
{: shortdesc}

当应用程序在 {{site.data.keyword.Bluemix_notm}} 上运行时，PORT 环境变量由 Cloud Foundry 分配。但是，当应用程序在本地运行时，PORT 未定义，因此您可以定义应用程序的端口。为避免冲突，请将应用程序在本地侦听的端口定义为不同于 {{site.data.keyword.Bluemix_notm}} 所用的端口。

在以下 **js** 文件示例中，使用的是 **3000** 作为该端口号。通过使用 **3000**，您可以在本地运行应用程序以用于测试，也可以在 {{site.data.keyword.Bluemix_notm}} 上运行应用程序，而无需进一步更改。

```
var port = (process.env.PORT || 3000);
```
{: codeblock}
