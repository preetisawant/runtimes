---

copyright:
  years: 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 Dynatrace 在 {{site.data.keyword.cloud_notm}} 中监视 Node.js
{: #using_dynatrace}

Dynatrace 是第三方服务，它提供对应用程序的监视。您可以将 Dynatrace 与 Node.js 应用程序集成，但 IBM 不提供对第三方服务的支持。有关更多信息，请参阅[第三方服务](../common/buildpackSupport.html#third-party)。

有关 Dynatrace 及其许可的信息，请参阅 [Dynatrace Application Monitoring ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.dynatrace.com/en/products/application-monitoring.html)。

将 Node.js 应用程序配置为使用 Dynatrace 时，Node.js 运行时会从 Dynatrace 站点获取 Dynatrace 平台即服务 (PaaS) 安装脚本，并会在运行应用程序时运行 Dynatrace 代理程序。要将 Dynatrace 与应用程序集成，需要创建用户提供的服务，然后将该服务绑定到应用程序。

## 将 Dynatrace 与应用程序集成

1. 登录到 Dynatrace 帐户，然后生成 PaaS 令牌。有关详细信息，请参阅 Dynatrace Cloud Foundry 应用程序监视文档中的[生成 PaaS 令牌 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/how-do-i-monitor-cloud-foundry-applications/) 部分。

  记下您的环境标识和令牌。
1. 通过运行以下命令，创建一个指向您的 Dynatrace 凭证的用户提供的服务。服务名称必须包含字符串 `dynatrace`，例如 `dynatrace-service`。

    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken"
    ```
    {: codeblock}
    
    **注：**请不要将 `environmentid` 或 `apitoken` 替换为您的凭证。运行该命令后，系统将提示您输入它们的值。

    如果使用 Dynatrace Managed，还需要添加 `apiurl` 字段来指定受管服务器的 API 端点。
    
    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken, apiurl"
    ```
    {: codeblock}
    
    运行该命令后，根据提示将 `apiurl` 设置为 `https://<YourManagedServerURL>/e/<environmentID>/api`。
    
1. 将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 后，将您创建的用户提供的服务绑定到应用程序。例如，使用以下命令：
    ```
    ibmcloud cf bs myApp dynatrace-service
    ```
    {: codeblock}

    **注**：绑定服务后，必须重新编译打包应用程序。

   或者，可以通过将用户提供的服务的名称添加到应用程序的 `manifest.yml` 文件的 `service` 部分，将服务绑定到应用程序。
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
