---

copyright:
  years: 2015, 2019
lastupdated: "2019-02-01"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 Beta 功能
{: #using_beta_features}

**重要信息**：从 Liberty for Java buildpack V3.28 开始，不再包含 Beta 运行时。  

Liberty Beta 功能让您可以提早使用未来 Liberty 发行版中可能会包含的新功能和编程模型。大部分 Beta 功能还可以在部署到 {{site.data.keyword.Bluemix}} 的应用程序中使用。

**重要信息**：Beta 功能仅用于开发和测试目的，而不能用于生产目的。有关完整的使用条款，请参阅 [Beta 许可协议](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html)。

|功能|
| ------ |
| `jdbc-4.3` |
| `logstashCollector-1.1` |
| `validator-1.0` |
{: caption="表 1. {{site.data.keyword.Bluemix_notm}} 上 Liberty for Java 中可用的 Liberty Beta 功能" caption-side="top"}

要在 {{site.data.keyword.Bluemix_notm}} 中使用 Liberty Beta 功能，需要执行以下操作：

1. [部署服务器目录或打包服务器](/docs/runtimes/liberty/optionsForPushing.html)，并在 server.xml 文件中启用一个或多个 Beta 功能，如以下示例中所示：

  ```
<server>
    <featureManager>
        <feature>jdbc-4.3</feature>
    </featureManager>
</server>
  ```
  {: .codeblock}

2.  将 `IBM_LIBERTY_BETA` 环境变量设置为 `true`。此变量会引导 Liberty buildpack 为您的应用程序安装并启用 Beta 功能。例如：
  * 使用 [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/ibmcloud/download_cli.html)：
    ```
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_BETA true
    ```
    {: .codeblock}

  * 或者，使用 `manifest.yml` 文件：
    ```
      env:
          IBM_LIBERTY_BETA: "true"
    ```
    {: .codeblock}

3. 将 `JBP_CONFIG_LIBERTY` 环境变量设置为 `"version: +"`。此变量会启用 [Liberty 每月运行时](/docs/runtimes/liberty/buildpackDefaults.html#liberty_versions)，其支持 Beta 功能。例如：
  * 使用 {{site.data.keyword.Bluemix_notm}} CLI 工具：
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ```
    {: .codeblock}

  * 或者，使用 `manifest.yml` 文件：
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
    ```
    {: .codeblock}

如果在现有应用程序上启用 Beta 功能，请不要忘记在设置环境变量后重新编译打包应用程序。
