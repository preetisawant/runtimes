---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 在本端執行 Node.js 應用程式
{: #hints}

設定要在本端執行 Node.js 應用程式的埠號，以致當您在 {{site.data.keyword.Bluemix}} 執行它時，不會產生衝突。
{: shortdesc}

當應用程式在 {{site.data.keyword.Bluemix_notm}} 上執行，PORT 環境變數是由 Cloud Foundry 配置。不過，當應用程式在本端執行時，不會定義 PORT，因此您可以針對應用程式定義埠。若要避免衝突，請定義應用程式在本端接聽的埠，不同於 {{site.data.keyword.Bluemix_notm}} 所使用的埠。

在 **js** 檔案的下列範例中，會使用 **3000** 作為埠號。藉由使用 **3000**，您可以在本端（若是進行測試）以及在 {{site.data.keyword.Bluemix_notm}} 上執行應用程式，而不必做進一步的變更。

```
var port = (process.env.PORT || 3000);
```
{: codeblock}
