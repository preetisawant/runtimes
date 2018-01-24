---

copyright:
  years: 2017
lastupdated: "2017-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# 使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 開發 Tomcat 應用程式

您也可以使用 {{site.data.keyword.eclipsetoolsfull}}，作為開發應用程式並將其部署至 {{site.data.keyword.Bluemix}} 的替代方式。IBM Eclipse Tools 提供可安裝至現有 Eclipse 環境的外掛程式，以協助將整合開發環境 (IDE) 與 {{site.data.keyword.Bluemix_notm}} 整合。

此程序會遵循與 Liberty [入門指導教學](getting-started.html)相同的一般步驟。您將使用 Eclipse，設定開發環境、在本端及雲端上部署應用程式，以及在應用程式中整合資料庫服務。

## 開始之前
{: #prereqs}

您需要下列帳戶及工具：
* [IBM Eclipse Tools for IBM Cloud ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}
* [Eclipse IDE for Java EE Developers ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}

如果已完成[入門指導教學](getting-started.md)，您可能已有這些工具及帳戶。在開始之前，請確定您也已經安裝並登錄下列項目：
* [{{site.data.keyword.Bluemix_notm}} 帳戶](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git-scm.com/downloads){: new_window}
* [Maven ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat 8.0.41 版 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}

## 步驟 1：複製範例應用程式
{: #clone}

請先複製範例應用程式 GitHub 儲存庫。
  ```bash
git clone https://github.com/IBM-Bluemix/get-started-tomcat
```
  {: pre}

## 步驟 2：建置應用程式的原始碼
{: #build_app}

使用 Maven 來建置原始碼，並執行產生的應用程式。

1. 在指令行上，將目錄切換至範例應用程式所在的目錄。

  ```
cd get-started-tomcat
```
  {: pre}

1. 使用 Maven 來安裝相依關係，並建置 .war 檔。

  ```
mvn clean install
  ```
  {: pre}

## 步驟 3：準備應用程式以進行部署
{: #prepare}

若要部署至 {{site.data.keyword.Bluemix_notm}}，它有助於設定 manifest.yml 檔案。manifest.yml 包括應用程式的基本資訊（例如名稱、配置給每一個實例的記憶體數量，以及路徑）。我們已在 `get-started-java` 目錄中提供範例 manifest.yml 檔案。

開啟 manifest.yml 檔案，然後將 `name` 從 `GetStartedJava` 變更為您的應用程式名稱 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>。
{: download}

```
  applications:
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/GetStartedTomcat.war
    buildpack: java_buildpack
  ```
{: codeblock}

在此 manifest.yml 檔案中，**random-route: true** 會為應用程式產生隨機路徑，以防止您的路徑與其他人發生衝突。如果您選擇這樣做，則可以將 **random-route: true** 取代為 **host: myChosenHostName**，並提供您選擇的主機名稱。[進一步瞭解...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 步驟 4：部署至 {{site.data.keyword.Bluemix_notm}}
{: #deploy}

將您的應用程式部署至下列其中一個 Bluemix 地區。為取得最佳延遲，請選擇最接近使用者的地區。

|地區|API 端點|
|:---------------|:-------------------------------|
| 美國南部|https://api.ng.bluemix.net|
| 英國| https://api.eu-gb.bluemix.net|
| 雪梨| https://api.au-syd.bluemix.net|
| 法蘭克福| https://api.eu-de.bluemix.net |

1. 將 `<API-endpoint>` 取代為您地區的端點，以設定 API 端點。
  ```
cf api <API-endpoint>
  ```
  {: pre}

1. 登入 {{site.data.keyword.Bluemix_notm}} 帳戶。
  ```
cf login
  ```
  {: pre}

  如果您無法使用 `cf login` 或 `bx login` 指令登入，因為您已有聯合使用者 ID，請使用 `cf login --sso` 或 `bx login --sso` 指令，用您的單一登入 ID 登入。若要進一步瞭解，請參閱[使用聯合 ID 登入](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id)。

## 步驟 5：使用 Eclipse 進行開發
{: #eclipse}

1. 確定您具有 [IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix)。

2. 移至**檔案 > 匯入 > Maven > 現有 Maven 專案**，以將 `get-started-java` 範例匯入至 Eclipse。

3. 建立 Tomcat 伺服器定義：
  - 在「伺服器」視圖中按一下滑鼠右鍵 ->「新建」->「伺服器」。
  - 選取 `Apache` -> `Tomcat v8.0 Server`。
  - 選擇 `tomcat-install-dir`。
  - 繼續使用預設選項來執行精靈，直到完成。

4. 在 Apache 伺服器本端執行應用程式：
  - 在 `GetStartedTomcat` 範例上按一下滑鼠右鍵，然後選取「執行身分」->「在伺服器中執行」選項。
  - 尋找並選取 localhost Tomcat 伺服器，然後按「完成」。
  - 只要幾秒鐘，應用程式應該就會在 http://localhost:8080/GetStartedTomcat/ 執行

5. 在 {{site.data.keyword.Bluemix_notm}} 上執行應用程式：
  - 在 `GetStartedTomcat` 範例上按一下滑鼠右鍵，然後選取「執行身分」->「在伺服器中執行」選項。
  - 尋找並選取 `{{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}}`，然後按「完成」。
  - 精靈將引導您進行部署選項。請務必選擇應用程式的唯一名稱。
  - 只要幾分鐘，應用程式應該就會在您選擇的 URL 執行。

現在，您已在本端及雲端上執行程式碼！

## 步驟 6：新增資料庫
{: #add_database}

接下來，我們會將 {{site.data.keyword.cloudantfull}} 資料庫新增至此應用程式並設定應用程式，因此，它可以在本端及 {{site.data.keyword.Bluemix_notm}} 上執行。

1. 在瀏覽器中，登入 {{site.data.keyword.Bluemix_notm}}。瀏覽至「儀表板」。按一下「名稱」直欄中的應用程式名稱，以選取該應用程式。
2. 依序按一下「連線」及「連接新服務」。
2. 在「資料及分析」區段中，選取 `{{site.data.keyword.cloudant_short_notm}}`，然後建立服務。
3. 系統提示時，請選取「重新編譯打包」。{{site.data.keyword.Bluemix_notm}} 將重新啟動應用程式，並使用 `VCAP_SERVICES` 環境變數將資料庫認證提供給應用程式。只有在應用程式於 {{site.data.keyword.Bluemix_notm}} 上執行時，才能使用此環境變數。

環境變數可讓您分開部署設定與原始碼。例如，您可以將資料庫密碼儲存在原始碼中所參考的環境變數內，而不要將資料庫密碼寫在程式中。[進一步瞭解...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 步驟 7：使用資料庫
{: #use_database}
我們現在即將更新本端程式碼，使其指向此資料庫。我們會將服務的認證儲存在內容檔中。只有在應用程式於本端執行時，才會使用此檔案。在 {{site.data.keyword.Bluemix_notm}} 中執行時，將會從 VCAP_SERVICES 環境變數中讀取認證。

1. 開啟 Eclipse，並開啟 src/main/resources/cloudant.properties 檔案：
  ```
  cloudant_url=
  ```
  {: pre}

2. 在瀏覽器中，開啟 {{site.data.keyword.Bluemix_notm}} 使用者介面，然後選取您的應用程式 ->「連線」-> Cloudant ->「檢視認證」

3. 只要將 `url` 從認證複製並貼入 `cloudant.properties` 檔案的 `url` 欄位中，並儲存變更。結果將如下：
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```

4. 在 Eclipse 中，從「伺服器」視圖重新啟動 Tomcat 伺服器。

  重新整理瀏覽器視圖：http://localhost:8080/GetStartedTomcat/ 您輸入至應用程式的任何名稱，現在都會新增至資料庫。

  本端應用程式及 {{site.data.keyword.Bluemix_notm}} 應用程式將會共用資料庫。在上述 push 指令輸出中所列的 URL 檢視 {{site.data.keyword.Bluemix_notm}} 應用程式。當您重新整理瀏覽器時，從任一應用程式新增的名稱應該會出現在這兩個應用程式中。

請記住，如果您不需要應用程式在 {{site.data.keyword.Bluemix_notm}} 上維持執行中，請停止它以避免產生任何非預期的費用。
{: tip}  
