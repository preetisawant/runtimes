---

copyright:
  years: 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dynatrace を使用した {{site.data.keyword.cloud_notm}} 内の Node.js のモニター
{: #using_dynatrace}

Dynatrace は、アプリケーションのモニタリングを提供するサード・パーティー・サービスです。 Dynatrace を Node.js アプリケーションに統合することは可能ですが、IBM はサード・パーティー・サービスに関するサポートは提供しません。詳しくは、[サード・パーティー・サービス](../common/buildpackSupport.html#third-party)を参照してください。

Dynatrace とそのライセンスについては、[Dynatrace の『Application Monitoring』 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.dynatrace.com/en/products/application-monitoring.html) を参照してください。

Node.js アプリケーションが Dynatrace を使用するように構成されている場合、Node.js ランタイムは Dynatrace サイトから Dynatrace Platform as a Service (PaaS) インストール・スクリプトを取得し、その Dynatrace エージェントをアプリケーションで実行します。Dynatrace をアプリケーションと統合するには、ユーザー提供サービスを作成してから、そのサービスをアプリケーションにバインドする必要があります。

## Dynatrace とアプリケーションの統合

1. Dynatrace アカウントにログインし、PaaS トークンを生成します。詳しくは、Dynatrace Cloud Foundry アプリケーションのモニターの資料で[『Generate PaaS token』 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/how-do-i-monitor-cloud-foundry-applications/)セクションを参照してください。

  環境 ID とトークンを書き留めます。
1. 次のコマンドを実行して、Dynatrace 資格情報を指すユーザー提供サービスを作成します。サービスの名前には、`dynatrace` という文字列が含まれている必要があります (`dynatrace-service` など)。

    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken"
    ```
    {: codeblock}
    
    **注:** `environmentid` および `apitoken` を資格情報で置き換えないでください。このコマンドを実行すると、その値の入力を求めるプロンプトが出されます。

    Dynatrace Managed を使用している場合は、管理対象サーバーの API エンドポイントを指定する `apiurl` フィールドも追加します。
    
    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken, apiurl"
    ```
    {: codeblock}
    
    コマンドの実行後にプロンプトが出たら、`apiurl` を `https://<YourManagedServerURL>/e/<environmentID>/api` に設定します。
    
1. アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュした後で、作成したユーザー提供サービスをアプリケーションにバインドします。 例えば、次のコマンドを使用します。
    ```
    ibmcloud cf bs myApp dynatrace-service
    ```
    {: codeblock}

    **注**: サービスのバインド後にアプリケーションを再ステージングする必要があります。

   あるいは、アプリケーションの `manifest.yml` ファイルの `service` セクションにユーザー提供サービスの名前を追加することによって、サービスをアプリケーションにバインドすることもできます。
   ```yaml
   ---
    applications:
    - path: .
      memory: 256M
      instances: 1
      name: myApp
      host: myApp
      disk_quota: 1024M
    services:
      - dynatrace-service
   ```
   {: codeblock}
