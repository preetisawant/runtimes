---

copyright:
  years: 2019
lastupdated: "2019-02-01"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用每月运行时
{: #using_monthly_runtime}

Liberty 每月运行时提供最新版本以及对新功能和编程模型的访问权。

要在 {{site.data.keyword.Bluemix_notm}} 中使用 Liberty 每月运行时，需要执行以下操作：

将 `JBP_CONFIG_LIBERTY` 环境变量设置为 `"version: +"`，并将环境变量 `IBM_LIBERTY_MONTHLY` 设置为 `true`。这两个变量将启用 [Liberty 每月运行时](/docs/runtimes/liberty/buildpackDefaults.html#liberty_versions)。例如：
  * 使用 {{site.data.keyword.Bluemix_notm}} CLI 工具：
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_MONTHLY true
    ```
    {: .codeblock}

  * 或者，使用 `manifest.yml` 文件：
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

如果要在现有应用程序上启用每月运行时，您可能需要在设置环境变量后删除并重新推送应用程序。
