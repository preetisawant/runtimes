---

copyright:
  years: 2019
lastupdated: "2019-02-01"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 月次ランタイムの使用
{: #using_monthly_runtime}

Liberty 月次ランタイムは、最新バージョンと、新機能およびプログラミング・モデルへのアクセスを提供します。

Liberty 月次ランタイムを {{site.data.keyword.Bluemix_notm}} で使用するには、以下を実行する必要があります。

`JBP_CONFIG_LIBERTY` 環境変数を `"version: +"` に設定し、`IBM_LIBERTY_MONTHLY` 環境変数を `true` に設定します。これらの変数は、[Liberty 月次ランタイム](/docs/runtimes/liberty/buildpackDefaults.html#liberty_versions)を有効にします。例えば、次のように指定します。
  * {{site.data.keyword.Bluemix_notm}} CLI ツールを使用します。
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_MONTHLY true
    ```
    {: .codeblock}

  * あるいは、`manifest.yml` ファイルを使用します。
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
          IBM_LIBERTY_MONTHLY: true
    ```

    ```
      env:
          JBP_CONFIG_LIBERTY: "[version: +, app_archive: {features: [javaee-8.0]}]"
          IBM_LIBERTY_MONTHLY: true
    ```
    {: .codeblock}

既存のアプリケーションで月次ランタイムを有効にする場合は、環境変数を設定した後でアプリケーションの削除と再プッシュが必要になる場合があります。
