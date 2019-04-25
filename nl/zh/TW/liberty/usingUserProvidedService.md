---

copyright:
  years: 2017, 2018
lastupdated: "2018-6-26"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

#在 {{site.data.keyword.cloud_notm}} 中搭配使用使用者提供的服務與 Liberty
{: #using_user_provided}

Cloud Foundry 會提供機制來連接及使用 {{site.data.keyword.Bluemix_notm}} 環境內不一定提供或可用的服務。
該機能是[使用者提供的服務](https://docs.cloudfoundry.org/devguide/services/user-provided.html)。

此文件假設：
  * 您有某個服務可用、
  * 您可以取得該服務的認證，以及說明連接至該服務以及該服務與範例 Getting-Started-Liberty 範例應用程式搭配使用所需的步驟

針對此討論，我們將使用 CloudantNoSQLDB 實例作為範例服務，以及建立使用者提供的服務以與其連接。

## 步驟 1：推送 Getting-Started 應用程式
{: #follow_getting_started}

遵循[入門指導教學](/docs/runtimes/liberty/getting-started.html)中的步驟，直到將應用程式推送至 {{site.data.keyword.Bluemix_notm}}。請在連接資料庫之前停止。

## 步驟 2：建立 CloudantNoSQLDB 實例
{: #create_cloudantnosqldb}

遵循[入門指導教學](/docs/runtimes/liberty/getting-started.html)中的步驟，以建立 CloudantNoSqLDB 實例

使用視圖認證選項，以從 CloudandNoSQLDB 複製認證。將那些認證儲存至本端檔案（例如，cloudant-creds）。

## 步驟 3：建立使用者提供的服務
若要使用 Getting-Started 應用程式，使用者提供服務的名稱必須包含 "cloudantNoSQLDB"。Getting-Started 應用程式將會剖析 VCAP 服務變數，並尋找名稱包含 "cloudantNoSQLDB" 的使用者提供服務。

        ibmcloud cf cups my-cloudantNoSQLDB-ups -p cloudant-creds

## 步驟 4：連結使用者提供的服務以及重新編譯打包應用程式
將使用者提供的服務連結至 getting-started 應用程式。

        ibmcloud cf bs GettingStartedLiberty my-cloudantNoSQLDB-ups

        ibmcloud cf restage GettingStartedLiberty

## 步驟 5：確認
瀏覽至您的應用程式，並確認您可以將多個名稱新增至 'name' 欄位。
