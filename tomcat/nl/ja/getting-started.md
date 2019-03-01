---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-05"

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

* {: download} Hello World サンプル・アプリケーションが {{site.data.keyword.Bluemix}} に正常にデプロイされました。  入門として、このステップバイステップのガイドに従って作業してください。 または、<a class="xref" href="http://bluemix.net" target="_blank" title="(サンプル・コードのダウンロード)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="アプリケーション・コードのダウンロード" />サンプル・コードをダウンロード</a>して、ご自身で探索してください。

この入門チュートリアルに従って、開発環境のセットアップ、ローカルおよび {{site.data.keyword.Bluemix}} でのアプリケーションのデプロイ、およびデータベース・サービスのアプリケーションへの統合を行います。

これらの資料全体で、Cloud Foundry CLI の参照が、{{site.data.keyword.Bluemix_notm}} CLI に更新されました。 {{site.data.keyword.Bluemix_notm}} CLI には、同じ使い慣れた Cloud Foundry コマンドがありますが、{{site.data.keyword.Bluemix_notm}} アカウントやその他のサービスとの統合が強化されています。 このチュートリアルには、{{site.data.keyword.Bluemix_notm}} CLI の入門情報があります。
{: tip}

## 始める前に
{: #prereqs}

以下が必要です。
* [{{site.data.keyword.Bluemix_notm}} アカウント](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/ibmcloud/download_cli.html)
* [Git ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git-scm.com/downloads){: new_window}
* [Maven ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat バージョン 8.0.41 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}


## ステップ 1: サンプル・アプリケーションを複製する
{: #clone}

リポジトリーを複製して、サンプル・アプリケーションがあるディレクトリーに変更します。
  ```
git clone https://github.com/IBM-Cloud/get-started-tomcat
  ```
{: codeblock}

  ```
cd get-started-tomcat
  ```
{: codeblock}

*get-started-tomcat* ディレクトリー内のファイルを詳細に調べて、内容をよく理解します。

## ステップ 2: アプリケーションをローカルで実行する
{: #run_locally}

アプリケーションをインストールするには、pom.xml ファイルで定義されているように依存関係をインストールして、.war ファイルをビルドする必要があります。

1. 依存関係をインストールします。
  ```
mvn clean install  
  ```
  {: codeblock}

1. GetStartedTomcat.war を `target` ディレクトリーから `tomcat-install-dir` `webapps` ディレクトリーにコピーします。

1. アプリケーションを実行します。  
  ```
<tomcat-install-dir>/bin/startup.bat|.sh
  ```
  {: codeblock}

1. 次の URL でアプリケーションを表示します。http://localhost:8080/GetStartedTomcat/

`shutdown.bat|.sh` を使用してアプリケーションを停止します。  コマンドの実行許可の付与が必要になる可能性があることに注意してください。
{: tip}

## ステップ 3: {{site.data.keyword.Bluemix_notm}} のデプロイメントのためにアプリケーションを準備する
{: #prepare}

{{site.data.keyword.Bluemix_notm}} にデプロイするには、manifest.yml ファイルをセットアップすると役に立つことがあります。 manifest.yml には、アプリケーションに関する基本的な情報 (名前、各インスタンス用に割り振るメモリー量、経路など) が含まれます。 `get-started-tomcat` ディレクトリーにサンプルの manifest.yml ファイルが用意されています。

manifest.yml ファイルを開き、`name` を `GetStartedTomcat` からご使用のアプリケーション名 <var class="keyword varname" data-hd-keyref="app_name">app_name</var> に変更します。
{: download}

  ```
  applications:
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/GetStartedTomcat.war
    buildpack: java_buildpack
  ```
  {: codeblock}

この manifest.yml ファイル内の **`random-route: true`** は、アプリケーション用にランダムな経路を生成して、経路が他と衝突するのを回避します。  任意のホスト名を指定して、**`random-route: true`** を **`host: myChosenHostName`** に置き換えることも選択できます。
{: tip}

## ステップ 4: アプリケーションをデプロイする
{: #deploy}

{{site.data.keyword.Bluemix_short}} CLI を使用してアプリケーションをデプロイできます。

1. {{site.data.keyword.Bluemix_short}} アカウントにログインし、API エンドポイントを選択します。

  ```
ibmcloud login
  ```
  {: codeblock}

  フェデレーテッド・ユーザー ID をお持ちの場合は、代わりに次のコマンドを使用して、シングル・サインオン ID でログインしてください。 詳しくは、[『フェデレーテッド ID を使用したログイン』](/docs/cli/login_federated_id.html)を参照してください。

  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. 次に、Cloud Foundry の組織およびスペースをターゲットにします。
  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  組織およびスペースがセットアップされていない場合は、[組織およびスペースの追加](/docs/account/orgs_spaces.html)を参照してください。
  {: tip}

1. *get-started-tomcat* ディレクトリー内から、アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュします。

  ```
ibmcloud cf push
  ```
  {: codeblock}

  これには約 2 分かかることがあります。 デプロイメント・プロセスでエラーが発生した場合、`ibmcloud cf logs <Your-App-Name> --recent` コマンドを使用してトラブルシューティングすることができます。

デプロイメントが完了すると、アプリケーションが実行中であることを示すメッセージが表示されます。  push コマンドの出力にリストされている URL でアプリケーションを表示します。  また、次のコマンドを発行して、アプリケーションの状況と URL を確認することもできます。

  ```
ibmcloud cf apps
  ```
  {: codeblock}

また、{{site.data.keyword.Bluemix_notm}} [リソース・リスト](https://cloud.ibm.com/resources)にアクセスしてアプリケーションを表示することもできます。

## ステップ 5: データベースを追加する
{: #add_database}

次に、{{site.data.keyword.cloudant_short_notm}} NoSQL データベースをこのアプリケーションに追加して、ローカルおよび {{site.data.keyword.Bluemix_notm}} 上で実行できるようにアプリケーションをセットアップします。

1. ブラウザーで {{site.data.keyword.Bluemix_notm}} にログインし、ダッシュボードに移動します。 **「リソースの作成」**を選択します。
1. 検索して **{{site.data.keyword.cloudant_short_notm}}** を見つけて、このサービスを選択します。
1. **「使用可能な認証方式 (Available authentication methods)」**で、**「レガシー資格情報と IAM の両方を使用する (Use both legacy credentials and IAM)」**を選択します。 他のフィールドについては、デフォルト設定のままでかまいません。 **「作成」**をクリックしてサービスを作成します。
1. ナビゲーションで、**「接続」**に移動して、**「接続の作成」**をクリックします。アプリケーションを選択し、**「接続」**をクリックします。
1. デフォルト値を使用して、**「アプリの接続および再ステージ」**をクリックしてデータベースをアプリケーションに接続します。プロンプトが表示されたら、**「再ステージ」**をクリックします。

   {{site.data.keyword.Bluemix_notm}} はアプリケーションを再始動し、`VCAP_SERVICES` 環境変数を使用してデータベース資格情報をアプリケーションに提供します。 アプリケーションに対してこの環境変数が使用可能なのは、アプリケーションが {{site.data.keyword.Bluemix_notm}} で実行されている場合のみです。

環境変数を使用すると、デプロイメント設定をソース・コードと分離することができます。 例えば、データベース・パスワードをハードコーディングする代わりに、それを環境変数に保管して、ソース・コードではその環境変数を参照するようにできます。
{: tip}

## ステップ 6: データベースを使用する
{: #use_database}

次に、このデータベースを指すようにローカル・コードを更新します。 サービス用の資格情報をプロパティー・ファイルに保管します。 このファイルは、アプリケーションがローカルで実行されている場合にのみ使用されます。 {{site.data.keyword.Bluemix_notm}} で実行されているときには、資格情報は `VCAP_SERVICES` 環境変数から読み取られます。

1. {{site.data.keyword.Bluemix_notm}} [リソース・リスト](https://cloud.ibm.com/resources)にアプリケーションが含まれているのを確認します。アプリケーションの「サービス詳細」ページで、サイドバーの**「接続」**をクリックします。{{site.data.keyword.cloudant_short_notm}} メニュー・アイコン (**&hellip;**) をクリックし、**「資格情報の表示」**を選択します。

2. 資格情報から `url` のみをコピーして、`cloudant.properties` ファイルの `url` フィールドに貼り付け、変更を保存します。
  ```
cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:codeblock}

3. サーバーを再始動します。

http://localhost:8080/GetStartedTomcat/ でブラウザー・ビューを最新表示します。 アプリケーションに入力するすべての名前がデータベースに追加されるようになります。

  ローカル・アプリケーションと {{site.data.keyword.Bluemix_notm}} アプリケーションはデータベースを共有します。 ブラウザーを最新表示すると、どちらかのアプリケーションから追加した名前が両方に表示されます。


予期しない課金が発生しないように、アプリケーションを {{site.data.keyword.Bluemix_notm}} で稼働中にしておく必要がない場合、アプリケーションを停止することを忘れないでください。
{: tip}  

## 次のステップ

* [チュートリアル](/docs/tutorials/index.html)
* [サンプル ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
