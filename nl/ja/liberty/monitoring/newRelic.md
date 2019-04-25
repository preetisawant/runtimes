---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-12"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# New Relic を使用した {{site.data.keyword.cloud_notm}} 内の Liberty のモニター
{: #new_relic}

New Relic は、アプリケーションのモニタリング・メトリックを提供するサード・パーティーのサービスです。 New Relic サービスが提供する内容について詳しくは、[New
Relic](http://newrelic.com/java)を参照してください。

[Java agent manual installation documentation](https://docs.newrelic.com/docs/agents/java-agent/installation/java-agent-manual-installation) によると、New Relic サービスを使用してモニターされる Java アプリケーションは、通常 New Relic エージェントとアカウントのライセンス・キーを使用してバンドルおよび構成する必要があります。 {{site.data.keyword.Bluemix}} 環境では、New Relic の使用許諾契約書とアカウントは、{{site.data.keyword.Bluemix_notm}} 内にサービス・インスタンスを作成することにより取得できます。 その後 Java アプリケーションを New Relic サービス・インスタンスにバインドすると、Liberty ビルドパックがアプリケーションを自動構成して、New Relic サービスでモニターする準備を行います。
具体的にはビルドパックは次のことを行います。

* アプリケーションに New Relic エージェントを提供する。
* VCAP_APPLICATION および VCAP_SERVICES アプリケーション環境変数からアプリケーション名とライセンス・キーを取得する。
* New Relic エージェントで要求されるプロパティーと構成テンプレートを構成する。

Liberty ビルドパックがアプリケーション用に生成したサンプル構成は以下のようになります。

```
    -javaagent:/home/vcap/app/.new_relic_agent/new_relic_agent-3.12.0.jar
    -Dnewrelic.home=/home/vcap/app/.new_relic_agent
    -Dnewrelic.config.license_key=123456
    -Dnewrelic.config.app_name=myapp
    -Dnewrelic.config.log_file_path=../../../../../logs
```
{: codeblock}


## ユーザー提供の New Relic サービスの追加
{: #add_user_provided_new_relic}

既存の New Relic アカウントとライセンス・キーがある場合は、「ユーザー提供のサービス」を使用して既存の New Relic サービスをアプリケーションにバインドできます。

1. 既存のライセンス・キーを使用してユーザー提供のサービス・インスタンスを作成します。  例えば、既存のライセンス・キーが 1234567 の場合、「create-user-provided-service」に {{site.data.keyword.Bluemix_notm}} CLI を使用して、以下のプロンプトでライセンス・キー 1234567 を入力できます。

  ```
    ibmcloud cf create-user-provided-service mynewrelic -p "licenseKey"
    licenseKey> 1234567
  ```
  {: codeblock}

2. ユーザー提供の New Relic サービス・インスタンスを使用してアプリケーションを {{site.data.keyword.Bluemix_notm}} にデプロイします。  ユーザー提供の New Relic サービス・インスタンスを使用するサンプル・アプリケーション・マニフェストは以下のようになります。
  <pre>
        &dash;&dash;&dash;
        applications:
        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
         - mynewrelic
  </pre>
  {: codeblock}

3. New Relic ダッシュボードにアクセスしてアプリケーション・メトリックを表示します。

New Relic サービスの自動構成は、ビルドバックのフレームワークを通じて使用可能にされるコンテナー管理サービスであるため、他のサービスの自動構成と異なります。  フレームワークを通じて使用可能にされるため、このサービスの自動構成は以下の 3 点で他のサービスと異なっています。
* オプトアウトはオプションではありません。
* サービス統合は Java エージェントである New Relic エージェントに依存します。 したがって、server.xml ファイルのクラウド変数とは対照的に、これは Java オプションから構成されます。
* 構成は VCAP_SERVICES および VCAP_APPLICATION の両方に依存します。
