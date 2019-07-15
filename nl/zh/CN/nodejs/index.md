---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Node.js
{: #nodejs_runtime}

{{site.data.keyword.Bluemix}} 上的 Node.js 运行时采用 sdk-for-nodejs buildpack 技术。
sdk-for-nodejs buildpack 为 Node.js 应用程序提供完整的运行时环境。
{: shortdesc}

应用程序在根目录中包含 **package.json** 文件时，会使用 sdk-for-nodejs buildpack。

应用程序必须侦听通过 PORT 环境变量分配给它的端口。
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} 提供 Node.js 入门模板应用程序。Node.js 入门模板应用程序是简单的 Node.js 应用程序，提供可用于您应用程序的模板。您可以体验该入门模板应用程序，对其进行更改并将更改推送到 {{site.data.keyword.Bluemix_notm}} 环境。请参阅[使用入门模板应用程序](../common/starter_app_usage.html)，以获取有关使用入门模板应用程序的帮助。

## 应用程序管理
{: #app_management}
{{site.data.keyword.Bluemix_notm}} 提供若干用于管理和调试 Node.js 应用程序的实用程序。请参阅[应用程序管理](../common/app_mng.html)，以获取完整详细信息。

# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}
* [Node.js ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://nodejs.org)
* [IBM API Connect](https://strongloop.com/)
