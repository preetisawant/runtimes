---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-03"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用測試版特性
{: #using_beta_features}

Liberty 測試版特性可讓您提早存取未來 Liberty 版本中可能包含的新功能及程式設計模型。大部分的測試版特性也可以用於已部署至 {{site.data.keyword.Bluemix}} 的應用程式。

**重要事項**：測試版特性僅針對開發及測試用途，無法用於正式作業。如需完整的使用條款，請參閱[測試版授權合約](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html)。

|特性|
| ------ |
| `appSecurity-3.0` |
| `audit-1.0` |
| `beanValidation-2.0` |
| `cdi-2.0` |
| `javaee-8.0` |
| `javaeeClient-8.0` |
| `jaxrs-2.1` |
| `jpa-2.2` |
| `jpaContainer-2.2` |
| `jsf-2.3` |
| `jsfContainer-2.3` |
| `jsonb-1.0` |
| `jsonbContainer-1.0` |
| `jsonp-1.1` |
| `jsonpContainer-1.1` |
| `logstashCollector-1.1` |
| `servlet-4.0` |
| `usageMetering-1.0` |
| `validator-1.0` |
| `webProfile-8.0` |
{: caption="表 1. {{site.data.keyword.Bluemix_notm}} 中 Liberty for Java 可用的 Liberty 測試版特性" caption-side="top"}

若要在 {{site.data.keyword.Bluemix_notm}} 中使用 Liberty 測試版特性，您需要執行下列動作：

1. 在 server.xml 檔案中啟用一個以上的測試版特性，以[部署伺服器目錄或包裝伺服器](optionsForPushing.html)，如下列範例所示：


  ```
<server>
    <featureManager>
        <feature>servlet-4.0</feature>
        <feature>webProfile-8.0</feature>
    </featureManager>
</server>
  ```
  {: .codeblock}

2.  將 `IBM_LIBERTY_BETA` 環境變數設為 `true`。此變數會指示 Liberty 建置套件，為您的應用程式安裝並啟用測試版特性。例如：
  * 使用 [{{site.data.keyword.Bluemix_notm}} CLI (../../cli/reference/bluemix_cli/download_cli.html)：
    ```
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_BETA true
    ```
    {: .codeblock}

  * 或者，使用 `manifest.yml` 檔案：
    ```
env:
          IBM_LIBERTY_BETA: "true"
```
    {: .codeblock}

3. 將 `JBP_CONFIG_LIBERTY` 環境變數設為 `"version: +"`。此變數會啟用可支援測試版特性的 [Liberty 每月運行環境](buildpackDefaults.html#liberty_versions)。例如：
  * 使用 {{site.data.keyword.Bluemix_notm}} CLI 工具：
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ```
    {: .codeblock}

  * 或者，使用 `manifest.yml` 檔案：
    ```
env:
          JBP_CONFIG_LIBERTY: "version: +"
```
    {: .codeblock}

如果您要在現有應用程式上啟用測試版特性，請記得在設定環境變數之後重新編譯打包應用程式。
