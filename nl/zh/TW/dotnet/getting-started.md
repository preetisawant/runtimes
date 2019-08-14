---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-20"
subcollection: "Dotnet"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# 入門指導教學
{: #getting_started}

* {: download} 恭喜，您已在 {{site.data.keyword.Bluemix}} 上部署 Hello World 範例應用程式！若要開始使用，請遵循本逐步手冊。或者，<a class="xref" href="http://bluemix.net" target="_blank" title="（下載範例程式碼）"><img class="hidden" src="../../images/btn_starter-code.svg" alt="下載應用程式碼" />下載範例程式碼</a>，並自行探索。

遵循本入門指導教學，您將設定開發環境、在本端及 {{site.data.keyword.Bluemix}} 上部署應用程式，以及在應用程式中整合 {{site.data.keyword.Bluemix}} 資料庫服務。

## 開始之前
{: #prereqs}

您需要下列各項：
* [{{site.data.keyword.Bluemix_notm}} 帳戶](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/ibmcloud/download_cli.html)
* [Git ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git-scm.com/downloads){: new_window}
* 從 [.NET Core 下載網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.microsoft.com/net/download/core) 安裝 .NET Core 2.2.2 SDK 2.2.104。

## 步驟 1：複製範例應用程式
{: #clone}

請先複製範例應用程式 GitHub 儲存庫。
  ```
git clone https://github.com/IBM-Cloud/get-started-aspnet-core
  ```
  {: codeblock}


## 步驟 2：在本端執行應用程式
{: #run_locally}

1. 在指令行上，將目錄切換至範例應用程式所在的目錄。

  ```
  cd get-started-aspnet-core/src/GetStartedDotnet
  ```
  {: codeblock}

1. 執行下列指令，在本端執行應用程式。

  ```
dotnet restore
  ```
  {: codeblock}

  ```
dotnet run
  ```
  {: codeblock}

1. 在下列網址檢視您的應用程式：http://localhost:5000/

## 步驟 3：準備應用程式以進行部署
{: #prepare}

若要部署至 {{site.data.keyword.Bluemix_notm}}，它有助於設定 manifest.yml 檔案。manifest.yml 包括應用程式的基本資訊（例如名稱、配置給每一個實例的記憶體數量，以及路徑）。我們已在 `get-started-dotnet` 目錄中提供範例 manifest.yml 檔案。

開啟 manifest.yml 檔案，然後將 `name` 從 `GetStartedDotnet` 變更為您的應用程式名稱 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>。
{: download}

  ```
 applications:
 - name: GetStartedDotnet
   random-route: true
   memory: 512M
  ```
  {: codeblock}

在此 manifest.yml 檔案中，**`random-route: true`** 會為應用程式產生隨機路徑，以防止您的路徑與其他人發生衝突。如果您選擇這樣做，則可以將 **`random-route: true`** 取代為 **`host: myChosenHostName`**，並提供您選擇的主機名稱。
{: tip}

## 步驟 4：部署應用程式
{: #deploy}

您可以使用 {{site.data.keyword.Bluemix_notm}} CLI 來部署應用程式。

1. 登入 {{site.data.keyword.Bluemix_notm}} 帳戶，然後選取 API 端點。
  ```
ibmcloud login
  ```
  {: codeblock}

  如果您有聯合使用者 ID，請改用下列指令，以使用單一登入 ID 登入。若要進一步瞭解，請參閱[使用聯合 ID 登入](/docs/cli/login_federated_id.html)。
 ```
ibmcloud login --sso
  ```
  {: codeblock}

1. 將目標設為 Cloud Foundry 組織及空間：
  ```
ibmcloud target --cf
  ```
  {: codeblock}

  如果您未設定組織或空間，請參閱[新增組織及空間](/docs/account/orgs_spaces.html)。
  {: tip}

1. **請確定您位於應用程式的主要目錄 `get-started-aspnet-core` 中**，然後將應用程式推送至 {{site.data.keyword.Bluemix_notm}}：
  ```
ibmcloud cf push
  ```
  {: codeblock}

  這可能需要一分鐘。如果部署處理程序發生錯誤，則您可以使用指令 `ibmcloud cf logs <Your-App-Name> --recent` 進行疑難排解。

部署完成之後，您應該會看到一則訊息，指出應用程式正在執行。在 push 指令輸出中所列的 URL 檢視應用程式。您也可以發出下列指令來檢視應用程式的狀態，以及查看 URL。
  ```
ibmcloud cf apps
  ```
  {: codeblock}

您也可以移至 {{site.data.keyword.Bluemix_notm}} [資源清單](https://cloud.ibm.com/resources)，以檢視應用程式。

## 步驟 5：新增資料庫
{: #add_database}

接下來，我們會將 {{site.data.keyword.cloudant_short_notm}} NoSQL Database 新增至此應用程式並設定應用程式，因此，它可以在本端及 {{site.data.keyword.Bluemix_notm}} 上執行。

1. 在瀏覽器中，登入 {{site.data.keyword.Bluemix_notm}}，並移至「儀表板」。選取**建立資源**。
1. 搜尋 **{{site.data.keyword.cloudant_short_notm}}**，並選取服務。
1. 針對**可用的鑑別方法**，選取**使用舊式認證及 IAM**。其他欄位可以保留預設值。按一下**建立**，以建立服務。
1. 在導覽中，移至**連線**，然後按一下**建立連線**。選取您的應用程式，然後按一下**連接**。
1. 使用預設值，按一下**連接並重新編譯打包應用程式**以將資料庫連接至您的應用程式。系統提示時，按一下**重新編譯打包**。

   {{site.data.keyword.Bluemix_notm}} 將重新啟動應用程式，並使用 `VCAP_SERVICES` 環境變數將資料庫認證提供給應用程式。只有在應用程式於 {{site.data.keyword.Bluemix_notm}} 上執行時，才能使用此環境變數。

環境變數可讓您分開部署設定與原始碼。例如，您可以將資料庫密碼儲存在原始碼中所參考的環境變數內，而不要將資料庫密碼寫在程式中。
{: tip}

## 步驟 6：在本端使用資料庫
{: #use_database}

我們現在即將更新本端程式碼，使其指向此資料庫。我們會將服務的認證儲存在 JSON 檔案中。只有在應用程式於本端執行時，才會使用此檔案。在 {{site.data.keyword.Bluemix_notm}} 中執行時，將會從 `VCAP_SERVICES` 環境變數中讀取認證。

1. 在 `src/GetStartedDotnet` 目錄中，建立 `vcap-local.json` 檔案。

1. 將下列 JSON 物件複製並貼到 `vcap-local.json` 檔案，然後儲存變更。

   ```json
   {
     "services": {
       "cloudantNoSQLDB": [
         {
           "credentials": {
             "url":"CLOUDANT_DATABASE_URL"
           },
           "label": "cloudantNoSQLDB"
         }
       ]
     }
   }
   ```
   {: codeblock}

1. 在 {{site.data.keyword.Bluemix_notm}} [資源清單](https://cloud.ibm.com/resources)中找到您的應用程式。在應用程式的「服務詳細資料」頁面上，按一下資訊看板中的**連線**。按一下 {{site.data.keyword.cloudant_short_notm}} 功能表圖示 (**&hellip;**)，然後選取**檢視認證**。

1. 只要將 `url` 值從認證複製並貼入 `vcap-local.json` 檔案的 `url` 欄位，並取代 `CLOUDANT_DATABASE_URL`。

1. 從 `get-started-aspnet-core/src/GetStartedDotnet` 目錄，執行下列指令來重新啟動應用程式。

   ```
   dotnet run
   ```
   {: codeblock}

1. 重新整理瀏覽器視圖：`http://localhost:5000/`。您輸入至應用程式的任何名稱，現在都會新增至資料庫。

本端應用程式及 {{site.data.keyword.Bluemix_notm}} 應用程式將會共用資料庫。在 `ibmcloud cf push` 指令輸出中所列的 URL 檢視 {{site.data.keyword.Bluemix_notm}} 應用程式。當您重新整理瀏覽器時，從任一應用程式新增的名稱應該會出現在這兩個應用程式中。

請記住，如果您不需要應用程式維持執行中，請停止它以避免產生任何非預期的費用。
{: tip}

## 後續步驟

* [指導教學](/docs/tutorials/index.html)
* [範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://ibm-cloud.github.io){: new_window}
* [架構中心 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
