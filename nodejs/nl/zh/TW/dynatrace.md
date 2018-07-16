---

copyright:
  years: 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 Dynatrace 在 {{site.data.keyword.cloud_notm}} 中監視 Node.js
{: #using_dynatrace}

Dynatrace 是協力廠商服務，可為您的應用程式提供監視功能。您可以整合 Dynatrace 與 Node.js 應用程式，但 IBM 不提供對協力廠商服務的支援。如需相關資訊，請參閱[協力廠商服務](../common/buildpackSupport.html#third-party)。

如需 Dynatrace 及其授權的相關資訊，請參閱 [Dynatrace Application Monitoring ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.dynatrace.com/en/products/application-monitoring.html)。

Node.js 應用程式配置成使用 Dynatrace 時，Node.js 運行環境會從 Dynatrace 網站獲得 Dynatrace 平台即服務 (PaaS) 安裝 Script，並且搭配執行該 Dynatrace 代理程式與您的應用程式。若要整合 Dynatrace 與您的應用程式，您需要建立使用者提供的服務，然後將服務連結至應用程式。

## 整合 Dynatrace 與您的應用程式

1. 登入 Dynatrace 帳戶，並產生 PaaS 記號。如需詳細資料，請參閱 Dynatrace Cloud Foundry 應用程式監視文件中的[產生 PaaS 記號 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/how-do-i-monitor-cloud-foundry-applications/) 一節。

  請記下您的環境 ID 及記號。
1. 執行下列指令，以建立可指向 Dynatrace 認證的使用者所提供服務。服務的名稱必須包含字串 `dynatrace`，例如 `dynatrace-service`。

    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken"
    ```
    {: codeblock}
    
    **附註：**請不要將 `environmentid` 或 `apitoken` 取代為您的認證。執行該指令之後，系統會提示您輸入其值。

    如果您是使用 Dynatrace Managed，則也會新增 `apiurl` 欄位，該欄位會指定「受管理伺服器」的 API 端點。
    
    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken, apiurl"
    ```
    {: codeblock}
    
    在您執行該指令之後系統提示時，請將 `apiurl` 設為 `https://<YourManagedServerURL>/e/<environmentID>/api`。
    
1. 將您的應用程式推送到 {{site.data.keyword.Bluemix_notm}} 之後，請將您建立的使用者所提供服務連結到該應用程式。例如，使用下列指令：
    ```
    ibmcloud cf bs myApp dynatrace-service
    ```
    {: codeblock}

    **附註**：您必須在連結該服務之後重新編譯打包應用程式。

   或者，您也可以將使用者提供的服務名稱新增至應用程式 `manifest.yml` 檔案的 `service` 區段，以將服務連結至您的應用程式。
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
