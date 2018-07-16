---

copyright:
  years: 2016, 2018
lastupdated: "2018-01-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Node.js 的工作離線模式
{: #offline_mode}

將 Node.js 應用程式推送至 {{site.data.keyword.Bluemix}} 之後，SDK for Node.js 建置套件通常會從外部資源下載構件，例如 NPM 提供的 Node 模組。在某些狀況下（例如使用 [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 及
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local)），您可以自訂對 {{site.data.keyword.Bluemix_notm}} 外部網站的存取。  
{: shortdesc}

Node.js 建置套件可以存取下列外部網站。您可能需要在 [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 及
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) {{site.data.keyword.Bluemix_notm}} 環境中，將這些網站列入*白名單*。

* http://nodejs.org/ 可用來確定可用的 node 引擎版本。
* https://s3pository.heroku.com 可用來擷取建置套件中沒有包含的 Node 引擎版本。
*  https://www.npmjs.com/package/npm 和 https://semver.herokuapp.com 可用來擷取建置套件中沒有包含的 npm 版本。
* https://iojs.org 可用來擷取建置套件中沒有包含，或是 https://semver.herokuapp.com 沒有提供的舊版 node。
* https://registry.npmjs.org 可用來擷取 Express 之類的 node 模組。

若要盡量精簡白名單網站集，請將您的應用程式配置為使用 SDK for Node.js 建置套件中包含的 Node 引擎版本。請參閱[最新更新項目](./updates.html)，以取得建置套件中包含的 Node 引擎版本集。如果您將應用程式配置為使用這些 Node 引擎版本，則只需要 https://registry.npmjs.org 網站即可下載模組。

請注意，安裝新版本的 SDK for Node.js 建置套件後，可用的引擎版本集通常就會變更為較新的版本。您可能需要重新配置您的應用程式，以指定建置套件中包含的較新 Node 引擎版本。


## 離線應用程式
{: #offline_applications}

若不想要存取 https://registry.npmjs.org，您可以將應用程式需要的所有 Node 模組併入您的應用程式中。若要這麼做，請針對所有必要的應用程式模組執行 `npm install`，然後將所產生的 *node_modules* 目錄併入您推送的應用程式中。

您的相依關係可以有相依關係，而這些相依關係還可以再有相依關係，一直延續下去，但是 `package.json` 只包含最上層相依關係。如果其中一個相依關係使用 package.json 中的範圍，而該檔案有發行新的版本，則 node_modules 目錄中的模組就會作廢。*Shrinkwrap* 可協助您鎖定所有相依關係版本，所以不會發生這種情形。若要使用 shrinkwrap，請從空的或乾淨的 `node_modules` 目錄開始進行。然後，在專案的根目錄中執行：


1. `npm install`
1. `npm dedupe`
2. `npm shrinkwrap`

這樣可能會變更您的 `package.json`，並且在您的根目錄中新增 `npm-shrinkwrap.json`。每當您變更 `package.json` 檔案中的相依關係時，就要重複 `npm dedupe` 及 `shringwrap` 步驟。

## 使用 Proxy
{: #working_with_proxy}

在一些如 [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 及 [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) 這類環境中，可以配置 Proxy。如需詳細資訊，請參閱[使用 Proxy](/docs/manageapps/workingWithProxy.html)。
