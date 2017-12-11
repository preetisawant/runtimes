---

copyright:
  years: 2015, 2017
lastupdated: "2017-06-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 可用的版本
{: #available_versions}

{{site.data.keyword.Bluemix}} 提供所有[目前可用的 Node.js 運行環境](http://nodejs.org/dist/)。在可用的運行環境中，IBM 提供了包含加強功能和錯誤修正程式的特定版本。如需支援版本的相關資訊，請參閱 [Node.js 建置套件的最新更新項目](/docs/runtimes/nodejs/updates.html)。
{: shortdesc}

IBM Node.js 建置套件會快取 IBM 運行環境版本。如果您在應用程式中使用 IBM SDK for Node.js 運行環境，當您將應用程式推送至 Bluemix 時，它會執行地更快。

## 指定版本

* 請在 **package.json** 檔案的 **engines** 區段中使用 **node** 參數，指定您要執行的 Node.js 運行環境版本。

* 如果您需要指定非 Node.js 組合版本的 npm 版本，請在 **package.json** 檔案的 **engines** 區段中使用 **npm** 參數。  

請參閱下列範例：

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

**附註：**node 版本應該一律指定在 **package.json** 檔案中。如果未指定，將使用最新的 node 版本。
