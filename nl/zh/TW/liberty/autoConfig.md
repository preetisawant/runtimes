---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 配置連結服務
{: #auto_config}

您可以將各種服務連結到您的 Liberty for Java 應用程式。依據開發人員的需求，服務可以由容器管理及/或由應用程式管理。

應用程式管理的服務是完全由應用程式管理的服務，沒有任何來自 Liberty 的協助。應用程式一般會讀取 VCAP_SERVICES，以取得已連結服務的相關資訊，並直接存取該服務。應用程式提供了所有必要的用戶端存取程式碼。與 Liberty 特性或 `server.xml` 檔案配置沒有任何相依關係。Liberty 建置套件自動配置不適用於此類型的服務。

容器管理的服務是由 Liberty 運行環境管理的服務。在某些情況下，應用程式可能會在 JNDI 中查閱已連結的服務，而在其他情況下，Liberty 會自己直接使用服務。Liberty 建置套件會讀取 VCAP_SERVICES，以取得已連結服務的相關資訊。針對每一個容器管理的服務，建置套件會執行三項功能。

* 為連結的服務產生[雲端變數](/docs/runtimes/liberty/optionsForPushing.html#accessing_info_of_bound_services)。
* 安裝 Liberty 特性及存取連結服務所需的用戶端存取程式碼。
* 產生或更新服務所需的 `server.xml` 檔案段落。

這個處理程序稱為自動配置。

Liberty 建置套件提供下列服務類型的自動配置：

* [{{site.data.keyword.autoscaling}}](/docs/services/Auto-Scaling/index.html#autoscaling)
* [ClearDB MySQL Database ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.cleardb.com/developers)
* [{{site.data.keyword.cloudant}}](/docs/services/Cloudant/index.html#Cloudant)
* [{{site.data.keyword.composeForMongoDB}}](/docs/services/ComposeForMongoDB/index.html)
* [{{site.data.keyword.composeForMySQL}}](/docs/services/ComposeForMySQL/index.html)
* [{{site.data.keyword.composeForPostgreSQL}}](/docs/services/ComposeForPostgreSQL/index.html)
* [{{site.data.keyword.dashdbshort}}](/docs/services/dashDB/index.html#dashDB)
* [ElephantSQL](/docs/services/ElephantSQL/index.html)
* [{{site.data.keyword.ssoshort}}](/docs/services/SingleSignOn/index.html#sso_gettingstarted)

Compose 服務可以是由容器管理或由應用程式管理。依預設，Liberty 建置套件會假設這些服務是由容器管理，並自動加以配置。如果您要讓應用程式管理服務，可以設定 `services_autoconfig_excludes` 環境變數，拒絕自動配置服務。如需相關資訊，請參閱[拒絕服務自動配置](/docs/runtimes/liberty/autoConfig.html#opting_out)。

## 安裝 Liberty 特性及用戶端存取程式碼
{: #installation_of_liberty_features}

當您連結至容器管理的服務時，該服務可能會要求得在 `server.xml` 檔案的 `featureManager` 段落中配置 Liberty 特性。Liberty 建置套件會更新 `featureManager` 段落，並安裝必要的支援二進位檔。如果服務需要用戶端驅動程式 JAR 檔，會將檔案下載到 Liberty 安裝中的已知位置。

請參閱[拒絕服務自動配置](#opting_out)一節，以取得連結服務類型的更多詳細資料。

## 產生或更新 server.xml 配置段落
{: #generating_or_updating_serverxml}

當您推送獨立式應用程式時，Liberty 建置套件可以在 `server.xml` 檔案中自動產生還是更新配置段落，需視您的應用程式與服務的連結方式，以及您是否有現有的 `server.xml` 檔案而定。

當您推送獨立式應用程式時，Liberty 建置套件會如[推送 Liberty 應用程式的選項](/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing)中所述，將 `server.xml` 配置段落產生到 {{site.data.keyword.Bluemix_notm}}。

當您推送獨立式應用程式並連結至容器管理的服務時，Liberty 建置套件會為已連結的服務產生必要的 `server.xml` 段落。

當您提供 `server.xml` 檔案並連結至容器管理的服務時，Liberty 建置套件會產生或更新配置段落。

* 如果所提供的 `server.xml` 檔案不包含已連結服務的配置段落，Liberty 會產生已連結服務的配置。
* 如果所提供的 `server.xml` 檔案包含已連結服務的配置段落，Liberty 會更新已連結服務的配置。

如需詳細資料，請參閱已連結之服務類型的文件。

## 拒絕服務自動配置
{: #opting_out}

在某些情況下，您可能會不想讓 Liberty 建置套件自動配置已連結的服務。請考慮下列情境。

* 我的應用程式使用 *dashDB*，但我想要應用程式直接管理資料庫連線。應用程式中包含必要的用戶端驅動程式 JAR 檔。我不想讓 Liberty 建置套件自動配置 *dashDB* 服務。
* 我有提供 `server.xml` 檔案，而且已經為 *cloudant* 實例提供配置段落，因為我需要非標準的資料來源配置。我不想要 Liberty 建置套件更新我的 `server.xml` 檔案，但是我仍然需要 Liberty 建置套件確定已經安裝適當的支援軟體。

若要拒絕自動服務配置，請使用 services_autoconfig_excludes 環境變數。您可以在 manifest.yml 中包括此環境變數，或使用 {{site.data.keyword.Bluemix_notm}} 用戶端設定它。

您可以針對每個服務類型來拒絕服務的自動配置。您可以選擇完全拒絕（例如在 *dashDB* 情境中）或只拒絕 `server.xml` 檔案配置更新（例如在 *cloudant* 情境中）。您為 services_autoconfig_excludes 環境變數指定的值是字串，如下所示。

* 字串可以包含一個以上服務的拒絕規格。
* 特定服務的拒絕規格是 service_type=option，其中：
  * service_type 是 VCAP_SERVICES 中所顯示的服務標籤。
  * option 是 `all` 或 `config`。
* 如果字串包含多個服務的拒絕規格，則必須以單一空格字元隔開個別拒絕規格。

請參閱下列 `services_autoconfig_excludes` 字串文法的範例：

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type（如同 VCAP_SERVICES 中顯示的服務標籤）
    <option> :: all | config
    <delimiter> :: one white space character
```
{: codeblock}

**重要事項**：您指定的服務類型必須符合出現在 VCAP_SERVICES 環境變數中的服務標籤。不接受空格。**重要事項**：在 `<service_type_specification>` 內不接受空格。唯一接受使用空格的情況是要隔開多個 `<service_type_specification>` 實例。

使用 **all** 選項可拒絕服務的所有自動配置動作，如同上述的 *dashDB* 情境。使用 **config** 選項只會拒絕配置更新動作，如同上述的 *cloudant* 情境。

以下是 `manifest.yml` 檔案中用於 *dashDB* 和 *cloudant* 情境的拒絕規格範例。

```
    env:
      services_autoconfig_excludes: dashDB=all

    env:
      services_autoconfig_excludes: cloudant=config

    env:
      services_autoconfig_excludes: cloudant=config dashDB=all
```
{: codeblock}

以下是如何使用指令行介面來為 `myapp` 應用程式設定 `services_autoconfig_excludes` 環境變數的範例。

```
    ibmcloud cf set-env myapp services_autoconfig_excludes cloudant=config
    ibmcloud cf set-env myapp services_autoconfig_excludes "cloudant=config dashDB=all"
```
{: codeblock}

若要在 VCAP_SERVICES 中尋找服務的 *label*，請發出如下範例的指令：

```
    ibmcloud cf env myapp
```
{: codeblock}

輸出包含類似下列內容的文字， 您可以在其中看到含有值 `elephantsql` 的 **label** 欄位：

```
   "elephantsql": [
   {
      "credentials": {
        "max_conns": "5",
      "uri":      "..."
   },
   "label": "elephantsql",

```
{: codeblock}

## 置換服務配置
{: #override_service_config}

在某些情況下，您可能要置換自動配置所產生之服務的預設配置。您可以使用 **LBP_SERVICE_CONFIG_xxxx** 環境變數來置換服務配置。如需完整環境變數名稱以及用來置換它們的範例語法，請參閱下表。例如，若要置換 *elephantSQL* 服務的預設版本，並將它設為 8.3.4.+ 版，請發出與下面類似的指令：

```
    ibmcloud cf set-env myapp LBP_SERVICE_CONFIG_POSTGRESQL "{driver: { version: 8.3.4.+ }}"
```
{: codeblock}

這個表格顯示 **service_type** 與 **LBP_SERVICE_CONFIG_xxxx** 環境變數名稱的對映。

<table>
<tr>
<th align="left">service_type</th>
<th align="left">環境變數名稱</th>
</tr>

<tr>
<td>Auto-Scaling</td>
<td>LBP_SERVICE_CONFIG_AUTO-SCALING</td>
</tr>

<tr>
<td>cleardb</td>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
</tr>

<tr>
<td>cloudantNoSQLDB</td>
<td>LBP_SERVICE_CONFIG_CLOUDANTNOSQLDB</td>
</tr>

<tr>
<td>compose-for-mongodb</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MONGO</td>
</tr>

<tr>
<td>compose-for-mysql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
</tr>

<tr>
<td>compose-for-postgresql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
</tr>

<tr>
<td>elephantsql</td>
<td>LBP_SERVICE_CONFIG_POSTGRESQL</td>
</tr>

<tr>
<td>SingleSignOn</td>
<td>LBP_SERVICE_CONFIG_SINGLESIGNON</td>
</tr>
</table>


下列表格顯示用於置換部分服務配置選項的語法：

<table>
<tr>
<th align="left">環境變數名稱</th>
<th align="left">配置語法</th>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>
</table>
