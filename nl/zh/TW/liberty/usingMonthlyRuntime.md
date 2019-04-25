---

copyright:
  years: 2019
lastupdated: "2019-02-01"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用每月運行環境
{: #using_monthly_runtime}

Liberty 每月運行環境會提供新功能及程式設計模型的最新版本及存取。

若要在 {{site.data.keyword.Bluemix_notm}} 中使用 Liberty 每月運行環境，您需要執行下列動作：

將 `JBP_CONFIG_LIBERTY` 環境變數設為 `"version: +"`，並將 `IBM_LIBERTY_MONTHLY` 環境變數設為 `true`。這些變數會啟用 [Liberty 每月運行環境](/docs/runtimes/liberty/buildpackDefaults.html#liberty_versions)。例如：
  * 使用 {{site.data.keyword.Bluemix_notm}} CLI 工具：
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_MONTHLY true
    ```
    {: .codeblock}

  * 或者，使用 `manifest.yml` 檔案：
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

如果您要在現有應用程式上啟用每月運行環境，則可能需要在設定環境變數之後刪除及重新推送應用程式。
