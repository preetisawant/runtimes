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

{{site.data.keyword.Bluemix}} 上的 Node.js 運行環境是採用 sdk-for-nodejs 建置套件的技術。
sdk-for-nodejs 建置套件為 Node.js 應用程式提供完整的運行環境。
{: shortdesc}

當應用程式的根目錄包含 **package.json** 檔案時，會使用 sdk-for-nodejs 建置套件。

應用程式必須接聽透過 PORT 環境變數指派給它的埠。
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} 提供 Node.js 入門範本應用程式。Node.js 入門範本應用程式是簡單的 Node.js 應用程式，提供可以讓您用於應用程式的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 {{site.data.keyword.Bluemix_notm}} 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](../common/starter_app_usage.html)。

## 應用程式管理
{: #app_management}
{{site.data.keyword.Bluemix_notm}} 提供若干公用程式來管理 Node.js 應用程式及進行除錯。如需完整的詳細資料，請參閱[應用程式管理](../common/app_mng.html)。
