---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用可能なバージョン
{: #available_versions}

{{site.data.keyword.Bluemix}} では、[現在使用可能な Node.js ランタイム](http://nodejs.org/dist/)のすべてが提供されます。 使用可能なランタイムのうち、{{site.data.keyword.IBM_notm}} では機能拡張およびバグ修正を含む特定のバージョンを提供しています。サポートされるバージョンについて詳しくは、『[Node.js ビルドパックに対する最新の更新](/docs/runtimes/nodejs/updates.html)』を参照してください。
{: shortdesc}

IBM Node.js ビルドパックは、{{site.data.keyword.IBM_notm}} ランタイム・バージョンをキャッシュに入れます。 アプリケーションで {{site.data.keyword.IBM_notm}} SDK for Node.js ランタイムを使用している場合は、アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュすると、アプリケーションのパフォーマンスが向上します。

## バージョンの指定

* 実行したい Node.js ランタイムのバージョンを指定するには、**package.json** ファイルの **engines** セクションで **node** パラメーターを使用します。

* Node.js にバンドルされたバージョン以外のバージョンの `npm` を指定する必要がある場合は、`package.json` ファイルの `engines` セクションで `npm` パラメーターを使用します。  

以下の例を参照してください。

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

**注:** ノード・バージョンは必ず `package.json` ファイル内に指定する必要があります。バージョンが指定されていない場合、最新のノード・バージョンが使用されます。
