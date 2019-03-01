---

copyright:
  years: 2017, 2018
lastupdated: "2018-6-26"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

#{{site.data.keyword.cloud_notm}} 内の Liberty でのユーザー提供サービスの使用
{: #using_user_provided}

Cloud Foundry には、{{site.data.keyword.Bluemix_notm}} 環境によって必ずしも提供されていない、または環境内で使用可能でないサービスに接続してそのサービスを使用するメカニズムが用意されています。その機能は、[ユーザー提供サービス](https://docs.cloudfoundry.org/devguide/services/user-provided.html)です。

本資料では、以下を想定しています。
  * 何らかの使用可能なサービスがある。
  * そのサービスの資格情報を取得できる。
以下で、Getting-Started-Liberty サンプル・アプリケーションを使用して、そのサービスに接続してサービスを使用するために必要なステップを説明します。

この説明のために、サービス例として CloudantNoSQLDB インスタンスを使用し、それに接続するためのユーザー提供サービスを作成します。

## ステップ 1: Getting-Started アプリケーションをプッシュする
{: #follow_getting_started}

[入門チュートリアル](/docs/runtimes/liberty/getting-started.html)のステップに従って、アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュします。データベースに接続する前に停止します。

## ステップ 2: CloudantNoSQLDB インスタンスを作成する
{: #create_cloudantnosqldb}

[入門チュートリアル](/docs/runtimes/liberty/getting-started.html)のステップに従って、CloudantNoSqLDB インスタンスを作成します。

資格情報の表示オプションを使用して、CloudandNoSQLDB から資格情報をコピーします。それらの資格情報をローカル・ファイル (例えば、cloudant-creds) に保存します。

## ステップ 3: ユーザー提供サービスを作成する
Getting-Started アプリケーションを操作するには、ユーザー提供サービスの名前に「cloudantNoSQLDB」が含まれている必要があります。Getting-Started アプリケーションは VCAP サービス変数を構文解析して、「cloudantNoSQLDB」を含む名前を持つユーザー提供サービスを探します。

        ibmcloud cf cups my-cloudantNoSQLDB-ups -p cloudant-creds

## ステップ 4: ユーザー提供サービスをバインドしてアプリケーションを再ステージする
ユーザー提供サービスを Getting-started アプリケーションにバインドします。

        ibmcloud cf bs GettingStartedLiberty my-cloudantNoSQLDB-ups

        ibmcloud cf restage GettingStartedLiberty

## ステップ 5: 確認する
アプリケーションを参照して、「name」フィールドに複数の名前を追加できることを確認します。
