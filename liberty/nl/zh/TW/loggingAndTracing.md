---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 配置記載和追蹤
{: #logging_tracing}

## 日誌檔
{: #log_files}

{{site.data.keyword.Bluemix}} 中提供標準 Liberty 日誌，例如 `messages.log` 或 `ffdc` 目錄，它們位於每一個應用程式實例的 `logs` 目錄中。這些日誌可以從 {{site.data.keyword.Bluemix_notm}} 主控台或透過 {{site.data.keyword.Bluemix_notm}} CLI 進行存取。例如：

* 若要存取應用程式的最新日誌，請執行下列指令：

  ```
  ibmcloud cf logs --recent <appname>
  ```
  {: codeblock}


* 若要查看應用程式的 `messages.log` 檔案，請執行下列指令：

  ```
  ibmcloud cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

您可以透過 Liberty 配置檔來設定記載層次和其他追蹤選項。如需相關資訊，請參閱[疑難排解 Liberty：記載和追蹤](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)。

## 使用追蹤及傾出功能
{: #using_trace_and_dump}

### 在 {{site.data.keyword.Bluemix_notm}} 主控台中使用追蹤及傾出（已淘汰）

您可以直接從 {{site.data.keyword.Bluemix_notm}} 主控台調整執行中應用程式的 Liberty 追蹤配置。此主控台也會提供要求與下載執行緒及資料堆傾出的功能。若要調整追蹤配置或要求傾出，請在 {{site.data.keyword.Bluemix_notm}} 主控台中選取 Liberty 應用程式，然後選擇導覽中的「運行環境」功能表。在「運行環境」視圖中，選取實例，然後按*追蹤* 或*傾出* 按鈕。若要調整追蹤層次，請參閱[疑難排解 Liberty：記載和追蹤](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)，以取得追蹤規格語法的詳細資料。

### 透過 SSH 變更追蹤配置

當您推送應用程式時，server.xml 檔案會包含預設內容 **updateTrigger**（設為 **polled**）和 **monitorInterval**（設為 1 分鐘）。Liberty 伺服器會自動配置為每分鐘檢查一次是否有 server.xml 的更新項目。

如需使用自訂 server.xml 推送 Liberty 應用程式的選項，請參閱[使用 server.xml 推送 Liberty 應用程式](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing)。

如需如何在 server.xml 設定動態更新，請參閱[控制動態更新](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window}。

請遵循下列步驟來變更追蹤配置：

1. 以 SSH 方式連接至您的應用程式

  ```
 ibmcloud cf ssh <appname> [-i instance_index]
  ```
  {: codeblock}

2. 編輯 server.xml 中的 `<logging traceSpecification="xxxx"/>`，以設定您想要的追蹤規格，例如，使用 *vi*：

  ```
vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: codeblock}

附註：server.xml 變更會在重新編譯打包或重新啟動時遺失，且只對您使用 ssh 進入的實例有效。

如需追蹤規格語法的詳細資料，請參閱[疑難排解 Liberty：記載和追蹤](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window}。

### 透過 SSH 觸發傾出

請使用下列指令，以利用 SSH 特性，透過 {{site.data.keyword.Bluemix_notm}} CLI 觸發執行緒及資料堆傾出：

  ```
 ibmcloud cf ssh <appname> -c "pkill -3 java"
  ```
  {: codeblock}

如需下載已產生之傾出檔案的詳細資料，請參閱下面的文件。

## 下載傾出檔案
{: #download_dumps}

各種傾出檔案預設會放在應用程式容器的 `dumps` 目錄中。請使用 {{site.data.keyword.Bluemix_notm}} CLI `ibmcloud cf ssh` 來檢視及下載傾出檔案。

* 若要查看已產生的傾出，請執行下列指令：

  ```
  ibmcloud cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* 若要下載傾出檔案，請執行下列指令：

  ```
  ibmcloud cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

您也可以使用 `scp` 及其他類似工具來檢視及下載傾出檔案。如需相關資訊，請參閱 [Accessing Apps with SSH ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html)。

# 相關鏈結
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Liberty 運行環境](index.html)
* [Liberty 概觀](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
