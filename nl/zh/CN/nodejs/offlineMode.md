---

copyright:
  years: 2016, 2018
lastupdated: "2018-07-12"
subcollection: "Nodejs"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 脱机使用 Node.js
{: #offline_mode}

将 Node.js 应用程序推送到 {{site.data.keyword.Bluemix}} 时，SDK for Node.js buildpack 通常会从外部资源下载工件，例如从 NPM 下载 Node 模块。在某些情境中，例如使用 [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 和 [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) 时，可以定制对 {{site.data.keyword.Bluemix_notm}} 外部站点的访问。  
{: shortdesc}

Node.js buildpack 可以访问以下外部站点。您可能需要在 [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 和 [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) {{site.data.keyword.Bluemix_notm}} 环境中，将这些站点列入*白名单*。

* `http://nodejs.org/`，可用于查明可用的节点引擎版本。
* `https://s3pository.heroku.com`，用于检索该 buildpack 中未包含的 Node 引擎版本。
*  `https://www.npmjs.com/package/npm` 和 `https://semver.herokuapp.com`，用于检索该 buildpack 中未包含的 npm 版本。
* `https://iojs.org`，用于检索该 buildpack 中未包含且 https://semver.herokuapp.com 上未提供的旧版节点。
* `https://registry.npmjs.org`，用于检索节点模块，例如 express。

要尽可能缩小列入白名单的站点集，请将应用程序配置为使用 SDK for Node.js buildpack 中包含的 Node 引擎版本。有关该 buildpack 中包含的 Node 引擎版本集，请参阅[最新更新](/docs/runtimes/nodejs/updates.html)。如果将应用程序配置为使用这些 Node 引擎版本，那么仅需要 https://registry.npmjs.org 站点来下载模块。

请注意，安装了新版本的 SDK for Node.js buildpack 后，可用引擎版本集通常会更改为更新的版本。您可能需要重新配置应用程序以指定 buildpack 中包含的更新的 Node 引擎版本。


## 脱机应用程序
{: #offline_applications}

为了不再需要访问 `https://registry.npmjs.org`，可以在应用程序中包含应用程序所需的所有 Node 模块。为此，请对所有必需的应用程序模块运行 `npm install`，然后将生成的 `node_modules` 目录包含在推送的应用程序中。

依赖项中可以包含依赖项，而被包含的依赖项还可以包含依赖项，依此类推，但 `package.json` 只包含顶层依赖项。如果某个依赖项使用了 package.json 中的某个范围，且该依赖项的新版本已发布，那么 `node_modules` 目录中的模块会变为过时。*shrinkwrap* 可帮助您锁定所有依赖项版本，避免发生上述情况。要使用 shrinkwrap，请首先清空或清除 `node_modules` 目录。然后，在项目的根目录中运行以下命令：

```
npm install
```
{: codeblock}

```
npm dedupe
```
{: codeblock}

```
npm shrinkwrap
```
{: codeblock}

这可能会更改您的 `package.json`，并将 `npm-shrinkwrap.json` 添加到您的根目录中。
每次对 `package.json` 文件中的依赖项进行更改后，请重新运行 `npm dedupe` 和 `shrinkwrap` 命令。

## 使用代理
{: #working_with_proxy}

在某些环境（如 [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 和
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local)）中，可以配置代理。有关更多详细信息，请参阅[使用代理](/docs/runtimes-common/workingWithProxy.html)。
