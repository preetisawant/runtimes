---

copyright:
  years: 2017
lastupdated: "2017-09-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# 入門チュートリアル
{: #getting_started}

* {: download} Hello World サンプル・アプリケーションが {{site.data.keyword.Bluemix}} に正常にデプロイされました。入門として、このステップバイステップのガイドに従って作業してください。または、<a class="xref" href="http://bluemix.net" target="_blank" title="(サンプル・コードのダウンロード)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="アプリケーション・コードのダウンロード" />サンプル・コードをダウンロード</a>して、ご自身で探索してください。

以下の Dotnet 入門チュートリアルに従って、開発環境のセットアップ、ローカルおよび {{site.data.keyword.Bluemix}} でのアプリケーションのデプロイ、および {{site.data.keyword.Bluemix}} データベース・サービスのアプリケーションへの統合を行います。

## 始める前に
{: #prereqs}

以下が必要です。
* [{{site.data.keyword.Bluemix_notm}} アカウント](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git-scm.com/downloads){: new_window}
* [dot.net Web サイト ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.microsoft.com/net/download/core) の説明に従って .NET Core SDK v1.0.4 をインストールします。

## ステップ 1: サンプル・アプリケーションを複製する
{: #clone}

アプリケーションの操作を開始する準備ができました。リポジトリーを複製して、サンプル・アプリケーションがあるディレクトリーに移動します。
  ```
git clone https://github.com/IBM-Bluemix/get-started-aspnet-core
  ```
  {: pre}
  ```
cd get-started-aspnet-core
  ```
  {: pre}

## ステップ 2: アプリケーションをローカルで実行する
{: #run_locally}

アプリケーションを実行します。
  ```
cd src/GetStartedDotnet
  ```
  {: pre}
  ```
dotnet restore
  ```
  {: pre}
  ```
dotnet run
  ```
  {: pre}

http://localhost:5000/ でアプリケーションを表示します。

## ステップ 3: デプロイメントのためにアプリケーションを準備する
{: #prepare}

{{site.data.keyword.Bluemix_notm}} にデプロイするには、manifest.yml ファイルをセットアップすると役に立つことがあります。manifest.yml には、アプリケーションに関する基本的な情報 (名前、各インスタンス用に割り振るメモリー量、経路など) が含まれます。`get-started-dotnet` ディレクトリーにサンプル manifest.yml ファイルが用意されています。

manifest.yml ファイルを開き、`name` を `GetStartedDotnet` からご使用のアプリケーション名 (<var class="keyword varname" data-hd-keyref="app_name">app_name</var>) に変更します。
{: download}

  ```
 applications:
 - name: GetStartedDotnet
   random-route: true
   memory: 512M
  ```
  {: codeblock}

この manifest.yml ファイル内の **random-route: true** は、アプリケーション用にランダムな経路を生成して、経路が他と衝突するのを回避します。任意のホスト名を指定して、**random-route: true** を **host: myChosenHostName** に置き換えることも選択できます。[詳細はこちら...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## ステップ 4: アプリケーションをデプロイする
{: #deploy}

Cloud Foundry CLI を使用してアプリケーションをデプロイできます。

まず、以下のように {{site.data.keyword.Bluemix_notm}} アカウントにログインします。
  ```
cf login
```
  {: pre}
  
  フェデレーテッド・ユーザー ID を使用しているために `cf login` または `bx login` のコマンドを使用してログインできない場合は、`cf login --sso` または `bx login --sso` のコマンドを使用し、シングル・サインオン ID を使ってログインしてください。詳しくは、[『フェデレーテッド ID を使用したログイン』](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id)を参照してください。

API エンドポイントを選択します。
  ```
cf api <API-endpoint>
  ```
  {: pre}

コマンド内の *API-endpoint* は以下のリストにある API エンドポイントのいずれかで置き換えてください。

|URL|地域|
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net| 米国南部|
| https://api.eu-de.bluemix.net  | ドイツ        |
| https://api.eu-gb.bluemix.net| 英国|
| https://api.au-syd.bluemix.net| シドニー|

**アプリケーションのルート・ディレクトリー `get-started-aspnet-core` で作業していることを確認し**、アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュします。
  ```
cf push
```
  {: pre}

これには時間がかかることがあります。デプロイメント・プロセスでエラーが発生した場合、`cf logs <Your-App-Name> --recent` コマンドを使用してトラブルシューティングすることができます。

デプロイメントが完了すると、アプリケーションが実行中であることを示すメッセージが表示されます。push コマンドの出力にリストされている URL でアプリケーションを表示します。また、以下のコマンドを実行することもできます。
  ```
cf apps
  ```
  {: pre}
  このコマンドにより、アプリケーションの状況と URL が表示されます。

## ステップ 5: MySQL データベースを接続する
{: connect_mysql}

次に、ClearDB MySQL データベースをこのアプリケーションに追加し、ローカルおよび Bluemix で実行できるようにアプリケーションをセットアップします。

1. ご使用のブラウザーで {{site.data.keyword.Bluemix_notm}} にログインします。`「ダッシュボード」`を参照します。`「名前」`列の名前をクリックして、アプリケーションを選択します。
2. `「接続」`、`「新規に接続」`の順にクリックします。
2. `「データおよび分析」`セクションで`「ClearDB MySQL Database」`を選択し、サービスを`「作成」`します。
3. プロンプトが出されたら、`「再ステージ」`を選択します。{{site.data.keyword.Bluemix_notm}} はアプリケーションを再始動し、`VCAP_SERVICES` 環境変数を使用してデータベース資格情報をアプリケーションに提供します。この環境変数は、アプリケーションが {{site.data.keyword.Bluemix_notm}} で実行されている場合にのみアプリケーションで使用できます。

環境変数を使用すると、デプロイメント設定をソース・コードと分離することができます。例えば、データベース・パスワードをハードコーディングする代わりに、環境変数にそれを保管して、ソース・コードではその環境変数を参照するようにできます。[詳細はこちら...](/docs/manageapps/depapps.html#app_env)
{: tip}

## ステップ 6: ローカルでデータベースを使用する
{: #use_database}

次に、このデータベースを指すようにローカル・コードを更新します。サービスの資格情報を json ファイルに保管します。このファイルは、アプリケーションがローカルで実行されている場合にのみ使用されます。{{site.data.keyword.Bluemix_notm}} で実行されているときには、資格情報は VCAP_SERVICES 環境変数から読み取られます。

1. ファイル src/GetStartedDotnet/vcap-local.json を作成します。

2. ブラウザーで {{site.data.keyword.Bluemix_notm}} UI を開き、「アプリ」->「接続」->「ClearDB MySQL Database」->「資格情報の表示」を選択します。

3. 資格情報の json オブジェクト全体を `vcap-local.json` ファイルにコピー・アンド・ペーストし、変更を保存します。結果は次のようになります。
  ```
  {
  "cleardb": [
    {
      "credentials": {
        ...
        "uri": "mysql://user:password@some-hostname.cleardb.net:3306/database-name?reconnect=true",
        ...
      },
      ...
      "name": "My ClearDB service instance name",
      ...
    }
  ]
}
  ```

4. `get-started-aspnet-core/src/GetStartedDotnet` ディレクトリーで `dotnet run` コマンドを使用して、アプリケーションを再始動します。

  http://localhost:5000/ のブラウザー・ビューを最新表示します。アプリケーションに入力するすべての名前がデータベースに追加されるようになります。

  ローカル・アプリケーションと {{site.data.keyword.Bluemix_notm}} アプリケーションは、データベースを共有しています。上の push コマンドの出力にリストされている URL で {{site.data.keyword.Bluemix_notm}} アプリケーションを表示します。いずれかのアプリケーションから追加した名前は、ブラウザーを最新表示すると両方に表示されます。

予期しない課金が発生しないように、アプリケーションを稼働中にしておく必要がない場合は停止することを忘れないでください。
{: tip}
