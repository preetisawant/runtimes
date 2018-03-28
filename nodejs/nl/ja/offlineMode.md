---

copyright:
  years: 2016, 2017, 2018
lastupdated: "2018-01-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Node.js のオフライン・モードの処理
{: #offline_mode}

Node.js アプリケーションが {{site.data.keyword.Bluemix}} にプッシュされると、SDK for Node.js ビルドパックは通常、NPM からの Node モジュールなど、外部リソースから成果物をダウンロードします。
[{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) や
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) などの状況によっては、{{site.data.keyword.Bluemix_notm}} 外部のサイトへのアクセスをカスタマイズすることができます。  
{: shortdesc}

Node.js ビルドパックは、以下の外部サイトにアクセスする可能性があります。[{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) および
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) の {{site.data.keyword.Bluemix_notm}} 環境で、これらのサイトを*ホワイトリスト登録*する必要がある場合があります。

* http://nodejs.org/ は、使用可能なノード・エンジン・バージョンを確認するために使用できます。
* https://s3pository.heroku.com は、ビルドパックに含まれていない Node エンジン・バージョンを取得するために使用します。
*  https://www.npmjs.com/package/npm および https://semver.herokuapp.com は、ビルドパックに含まれていないバージョンの npm を取得するために使用します。
* https://iojs.org は、ビルドパックに含まれておらず、https://semver.herokuapp.com でも入手できない、旧バージョンのノードを取得するために使用します。
* https://registry.npmjs.org は、express などのノード・モジュールを取得するために使用します。

ホワイトリストに登録される一連のサイトを最小限にするために、SDK for Node.js ビルドパックに含まれている Node エンジン・バージョンを使用するようにアプリケーションを構成してください。ビルドパックに含まれている一連の Node エンジン・バージョンについては、[最新の更新](./updates.html)を参照してください。これらの Node エンジン・バージョンを使用するようにアプリケーションを構成する場合、モジュールのダウンロードに必要なのは https://registry.npmjs.org サイトのみです。

新しいバージョンの SDK for Node.js ビルドパックをインストールすると、多くの場合、使用可能な一連のエンジン・バージョンが新しいバージョンに変更されることに注意してください。ビルドパックに含まれる新しい Node エンジン・バージョンを指定するように、アプリケーションの再構成が必要な場合があります。


## オフライン・アプリケーション
{: #offline_applications}

https://registry.npmjs.org にアクセスする必要がないようにするために、アプリケーションに必要な Node モジュールのすべてをアプリケーション内に組み込むことができます。これを行うには、必要なすべてのアプリケーション・モジュールを対象に `npm install` を実行し、結果として生じる *node_modules* ディレクトリーを、プッシュされるアプリケーションに組み込みます。

ご使用の依存関係にはそれぞれに依存関係が存在する可能性があり、それらの依存関係にはさらに依存関係が存在する可能性がありますが、`package.json` にはトップレベルの依存関係のみが含まれています。
いずれかの依存関係が package.json 内の範囲を使用していて、その範囲の新規バージョンがリリースされた場合、node_modules ディレクトリー内のモジュールがサポートされなくなる可能性があります。 *shrinkwrap* を使用すると、すべての依存関係バージョンをロックして、このような状態が起こらないようにするのに役立ちます。  shrinkwrap を使用するには、空の、またはクリーンアップされた `node_modules` ディレクトリーで始めます。その後、プロジェクトのルート・ディレクトリーで以下を実行します。


1. ```npm install```
1. ```npm dedupe```
2. ```npm shrinkwrap```

これにより、`package.json` を変更して、ルート・ディレクトリーに `npm-shrinkwrap.json` を追加することができます。
`package.json` ファイル内の依存関係を変更するたびに、`npm dedupe` と `shringwrap` のステップを繰り返します。

## プロキシーの処理
{: #working_with_proxy}

[{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) や [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) などの一部の環境では、プロキシーを構成できます。
詳しくは、[『プロキシーの処理』](/docs/manageapps/workingWithProxy.html)を参照してください。
