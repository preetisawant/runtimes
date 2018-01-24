---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 可用版本
{: #available_versions}

{{site.data.keyword.Bluemix}} 提供所有[目前可用的 Node.js 运行时](http://nodejs.org/dist/)。在可用的运行时中，{{site.data.keyword.IBM_notm}} 提供的特定版本包含增强功能和错误修订。请参阅 [Node.js Buildpack 的最新更新](/docs/runtimes/nodejs/updates.html)，以获取有关受支持版本的更多信息。
{: shortdesc}

IBM Node.js buildpack 高速缓存 {{site.data.keyword.IBM_notm}} 运行时版本。如果在应用程序中使用 {{site.data.keyword.IBM_notm}} SDK for Node.js 运行时，那么在将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 时应用程序执行速度更快。

## 指定版本

* 使用 **package.json** 文件的 **engines** 部分中的 **node** 参数，可指定要运行的 Node.js 运行时版本。

* 如果需要指定一个未与 Node.js 捆绑的 npm 版本，请使用 **package.json** 文件中 **engines** 部分内的 **npm** 参数。  

请参阅以下示例：

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}

**注：**应该始终在 **package.json** 文件中指定节点版本。如果未指定，那么将使用最新的节点版本。
