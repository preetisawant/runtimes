---

copyright:
  years: 2016, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# node.js のオフライン・モードの処理
{: #offline_mode}

node.js アプリケーションが {{site.data.keyword.Bluemix}} にプッシュされると、SDK for Node.js ビルドパックは通常、NPM からのノード・モジュールなど、外部リソースから成果物をダウンロードします。  [{[site.data.keyword.Bluemix_dedicated_notm](/docs/dedicated/index.html#dedicated) や [Bluemix_local_notm](/docs/local/index.html#local) を使用するような一部の状況では、{{site.data.keyword.Bluemix_notm}} の外部のサイトへのアクセスに依存しないようにしたり、そのようなサイトへのアクセスをより明示的に制御することもできます。  
{: shortdesc}

node.js ビルドパックによるアクセスが可能な外部サイトを以下に示します。  [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 環境と [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) {{site.data.keyword.Bluemix_notm}} 環境では、これらのサイトが*ホワイトリスト*に登録されていなければならないことがあります。

* http://nodejs.org/ は、使用可能なノード・エンジン・バージョンを確認するために使用できます。
* https://s3pository.heroku.com は、ビルドパックに含まれていないノード・エンジン・バージョンを取得するために使用します。
*  https://www.npmjs.com/package/npm および https://semver.herokuapp.com は、ビルドパックに含まれていないバージョンの npm を取得するために使用します。
* https://iojs.org は、ビルドパックに含まれておらず、https://semver.herokuapp.com でも入手できない、旧バージョンのノードを取得するために使用します。
* https://registry.npmjs.org は、express などのノード・モジュールを取得するために使用します。

ホワイトリストに登録される一連のサイトを最小限にするために、SDK for Node.js ビルドパックに含まれているノード・エンジン・バージョンを使用するようにノード・アプリケーションを構成してください。  ビルドパックに含まれている一連のノード・エンジン・バージョンについては、 [最新の更新](./updates.html)を参照してください。  そのように構成された場合には、ノード・モジュールをダウンロードするために必要なサイトは https://registry.npmjs.org のみになります。

新しいバージョンの SDK for Node.js ビルドパックをインストールすると、多くの場合、使用可能な一連のノード・エンジン・バージョンが新しいバージョンに移行することに注意してください。  その結果、ノード・アプリケーションを再構成して、新しいノード・エンジン・バージョンを指定することが必要になる場合があります。


## オフライン・アプリケーション
{: #offline_applications}

https://registry.npmjs.org にアクセスする必要がないようにするために、アプリケーションに必要なノード・モジュールのすべてをアプリケーション内に組み込むことができます。  これを行うには、プッシュされたアプリケーションを使用して、アプリケーションに必要なすべてのモジュールを対象に **npm install** を実行し、結果として生じる *node_modules* ディレクトリーを組み込みます。

ご使用の依存関係にはそれぞれに依存関係が存在する可能性があり、それらの依存関係にはさらに依存関係が存在する可能性があるというようになっていますが、package.json にはトップレベルの依存関係のみが含まれています。 いずれかの依存関係が package.json 内の範囲を使用していて、その範囲の新規バージョンがリリースされた場合、node_modules ディレクトリー内のモジュールがサポートされなくなる可能性があります。 *shrinkwrap* を使用すると、すべての依存関係バージョンをロックして、このような状態が起こらないようにするのに役立ちます。  shrinkwrap を使用するには、空の、またはクリーンアップされた node_modules ディレクトリーから始めて、プロジェクトのルート・ディレクトリーで以下を実行します。
0. npm install
1. npm dedupe
2. npm shrinkwrap

これにより、*package.json* を変更して、ルート・ディレクトリーに *npm-shrinkwrap.json* を追加することができます。
*package.json* ファイル内の依存関係を変更するたびに、*dedupe* と *shringwrap* のステップを繰り返します。

## プロキシーの処理
{: #working_with_proxy}

[{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) や [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) などの一部の環境では、プロキシーを構成できます。詳しくは、[『プロキシーの処理』](/docs/manageapps/workingWithProxy.html)を参照してください。
