---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-03"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# 使用 IBM Eclipse Tools for {{site.data.keyword.cloud_notm}} 開發應用程式

您也可以使用 {{site.data.keyword.eclipsetoolsfull}}，作為開發應用程式並將其部署至 {{site.data.keyword.Bluemix}} 的替代方式。{{site.data.keyword.eclipsetoolsfull}} 提供可安裝至現有 Eclipse 環境的外掛程式，以協助將整合開發環境 (IDE) 與 {{site.data.keyword.Bluemix_notm}} 整合。

此程序會遵循與 Liberty [入門指導教學](getting-started.html)相同的一般步驟。您將使用 Eclipse，設定開發環境、在本端及雲端上部署應用程式，以及在應用程式中整合 {{site.data.keyword.Bluemix_notm}} 資料庫服務。

## 開始之前
{: #prereqs}

您需要下列帳戶及工具：
* [IBM Eclipse Tools for IBM Cloud ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}
* [Eclipse IDE for Java EE Developers ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}

如果已完成[入門指導教學](getting-started.md)，您可能已有這些工具及帳戶。在開始之前，請確定您也已經安裝並登錄下列項目：
* [{{site.data.keyword.Bluemix_notm}} 帳戶](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} CLI](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git-scm.com/downloads){: new_window}
* [Maven ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://maven.apache.org/download.cgi){: new_window}

## 步驟 1：複製範例應用程式
{: #clone}

請先複製範例應用程式 GitHub 儲存庫。

  ```
git clone https://github.com/IBM-Cloud/get-started-java
  ```
  {: codeblock}

## 步驟 2：建置應用程式的原始碼
{: #build_app}

使用 Maven 來建置原始碼，並執行產生的應用程式。

1. 在指令行上，將目錄切換至範例應用程式所在的目錄。

  ```
cd get-started-java
  ```
  {: codeblock}

1. 使用 Maven 來安裝相依關係，並建置 .war 檔。

  ```
mvn clean install
  ```
  {: codeblock}

## 步驟 3：準備應用程式以進行部署
{: #prepare}

若要部署至 {{site.data.keyword.Bluemix_notm}}，它有助於設定 manifest.yml 檔案。manifest.yml 包括應用程式的基本資訊（例如名稱、配置給每一個實例的記憶體數量，以及路徑）。我們已在 `get-started-java` 目錄中提供範例 manifest.yml 檔案。

開啟 manifest.yml 檔案，然後將 `name` 從 `GetStartedJava` 變更為您的應用程式名稱 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>。
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

在此 manifest.yml 檔案中，**random-route: true** 會為應用程式產生隨機路徑，以防止您的路徑與其他人發生衝突。如果您選擇這樣做，則可以將 **random-route: true** 取代為 **host: myChosenHostName**，並提供您選擇的主機名稱。
{: tip}

## 步驟 4：登入 {{site.data.keyword.Bluemix_notm}}
{: #deploy}

1. 登入 {{site.data.keyword.Bluemix_notm}} 帳戶，然後選取 API 端點。

  ```
ibmcloud login
  ```
  {: codeblock}

  如果您因具有聯合使用者 ID 而無法使用 `ibmcloud login` 登入，則請使用下列指令，以您的單一登入 ID 登入。若要進一步瞭解，請參閱[使用聯合 ID 登入](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id)。

  ```
ibmcloud login --sso
  ```
  {: codeblock}

  接下來，將目標設為 Cloud Foundry CLI：

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  如果您未設定組織或空間，請參閱[新增組織及空間](https://console.bluemix.net/docs/account/orgs_spaces.html)。
  {: tip}

## 步驟 5：使用 Eclipse 進行開發
{: #eclipse}

1. 確定您具有 [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix)。

2. 移至**檔案 > 匯入 > Maven > 現有 Maven 專案**，以將 `get-started-java` 範例匯入至 Eclipse。

3. 建立 Liberty 伺服器定義。下列步驟將會下載新的 Liberty 伺服器。
  - 在**視窗 > 顯示視圖 > 伺服器**視圖中，按一下滑鼠右鍵選取**新建 > 伺服器**。
  - 選取 **IBM > WebSphere Application Server Liberty**。
  - 選取**從保存檔或儲存庫安裝**。
  - 系統提示時，請輸入您要安裝 Liberty 之新資料夾的目的地路徑 (/Users/username/liberty)。
  - 選取**從 ibm.com 下載及安裝新的運行環境**。
  - 選取**含 Java EE 7 Web 設定檔的 WAS Liberty**。
  - 繼續使用預設選項來執行精靈，直到完成。

4. 在 Liberty 本端執行應用程式：
  - 移至**視窗 > Web 瀏覽器 > 預設系統 Web 瀏覽器**，以將 Web 瀏覽器變更為系統預設值。
  - 用滑鼠右鍵按一下 `GetStartedJava` 範例，然後選取**執行身分 > 在伺服器中執行**。
  - 尋找並選取 localhost Liberty 伺服器，然後按一下**完成**。

  只要幾秒鐘，應用程式就會在 http://localhost:9080/GetStartedJava 執行。

5. 更新程式碼：
  - 開啟 `src/main/webapp/index.html`，並將標題從 `<h1>Welcome.</h1>` 更新為 `<h1>Welcome Jane.</h1>`。
  - 儲存變更。Liberty 會自動反映變更。
  - 重新整理瀏覽器 (`http://localhost:9080/GetStartedJava`)，以查看變更。

6. 將變更推送至 {{site.data.keyword.Bluemix_notm}}：
  - 在指令行上，從 `get-started-java` 目錄中，重建 .war 檔。

    ```
mvn clean install
    ```
    {: codeblock}

  - 將應用程式推送至 {{site.data.keyword.Bluemix_notm}}。

    ```
ibmcloud cf push
    ```
    {: codeblock}

現在，您已在本端及雲端上執行程式碼！

## 步驟 6：新增資料庫
{: #add_database}

接下來，我們會將 NoSQL Database 新增至此應用程式並設定應用程式，因此，它可以在本端及 {{site.data.keyword.Bluemix_notm}} 上執行。

1. 在瀏覽器中，登入 {{site.data.keyword.Bluemix_notm}}，並移至「儀表板」。選取**建立資源**。
2. 選擇**資料及分析**區段，然後選取 **{{site.data.keyword.cloudant_short_notm}}** 並建立服務。
3. 移至**連線**視圖並選取應用程式，然後**建立連線**。
4. 系統提示時，請選取**重新編譯打包**。{{site.data.keyword.Bluemix_notm}} 將重新啟動應用程式，並使用 `VCAP_SERVICES` 環境變數將資料庫認證提供給應用程式。只有在應用程式於 {{site.data.keyword.Bluemix_notm}} 上執行時，才能使用此環境變數。

環境變數可讓您分開部署設定與原始碼。例如，您可以將資料庫密碼儲存在原始碼中所參考的環境變數內，而不要將資料庫密碼寫在程式中。
{: tip}

## 步驟 7：使用資料庫
{: #use_database}
我們現在即將更新本端程式碼，使其指向此資料庫。我們會將服務的認證儲存在內容檔中。只有在應用程式於本端執行時，才會使用此檔案。在 {{site.data.keyword.Bluemix_notm}} 中執行時，將會從 `VCAP_SERVICES` 環境變數中讀取認證。

1. 在 Eclipse 中，開啟 src/main/resources/cloudant.properties 檔案：

  ```
  cloudant_url=
  ```
  {: codeblock}

2. 在瀏覽器中，移至 {{site.data.keyword.Bluemix_notm}}，然後選取**應用程式 > _您的應用程式_ > 連線 > Cloudant > 檢視認證**。

3. 只要將 `url` 從認證複製並貼入 `cloudant.properties` 檔案的 `url` 欄位中，並儲存變更。

  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:codeblock}

4. 在 Eclipse 中，從「伺服器」視圖重新啟動 Liberty 伺服器。

  重新整理瀏覽器視圖：`http://localhost:9080/GetStartedJava/`。您輸入至應用程式的任何名稱，現在都會新增至資料庫。

  本端應用程式及 {{site.data.keyword.Bluemix_notm}} 應用程式將會共用資料庫。當您重新整理瀏覽器時，從任一應用程式新增的名稱就會出現在這兩個應用程式中。


請記住，如果您不需要應用程式在 {{site.data.keyword.Bluemix_notm}} 上維持執行中，請停止應用程式以避免產生任何非預期的費用。
{: tip}  
