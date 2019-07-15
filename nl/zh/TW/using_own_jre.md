---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用您自己的 JRE
{: #using_own_jre}

您可以使用自己的 JRE 在 {{site.data.keyword.Bluemix}} 上執行 Liberty 應用程式。您必須完成下列動作，讓您的 JRE 可供您的應用程式使用。
* 在可供建置套件下載的位置管理 JRE。
* 管理提供 JRE 位置的 `index.yml` 檔案。
* 將您的應用程式配置為使用您的 JRE。

## 管理 JRE 及 `index.yml`
{: #hosting_jre}

您必須管理 Web 伺服器上可從中下載 Liberty 建置套件的 JRE 檔案。您可以使用任何可用的伺服器機能，在 {{site.data.keyword.Bluemix_notm}} 上管理它，也可以在公用的位置上管理它。必須以指定 JRE 檔相關詳細資料的 `index.yml` 檔案來配置伺服器。

完成下列步驟，以管理 JRE 及 `index.yml` 檔案：
  1. 獲得 JRE，其版本必須是用於 UNIX 64 位元作業系統的版本，而且必須是 `tar.gz` 檔案。
  2. 在 Liberty 建置套件可下載的位置管理 JRE 檔案。
  3. 在管理位置提供 `index.yml` 檔案。`index.yml` 檔案必須包括一個項目，其中包含 JRE 的版本 ID，後面接著一個冒號，以及完整的 JRE 檔位置 URL。
    * 在 `index.yml` 檔案中定義 JRE 版本。

    ```
    ---
    jre_version: https://hostingLocation/jreName.tar.gz
    ```
    {: codeblock}

    * 包括 JRE 版本 ID 及完整的 JRE 檔案位置。例如：

    ```
    ---
    1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```
    {: codeblock}

## 配置應用程式
{: #configure_app}

您必須在 Liberty 應用程式上設定兩個環境變數，將建置套件配置為使用替代 JRE。設定 **JBP_CONFIG_OPENJDK**，以識別 `index.yml` 檔案的位置，並將 **JVM** 環境變數設為 *openjdk*。如需 version-value 字串格式的相關資訊，請參閱 Cloud Foundry 文件中的[版本語法及排序以及萬用字元 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/util-repositories.md){: new_window}。

**JBP_CONFIG_OPENJDK** 變數的值為 `index.yml` 檔案位置，以及要從 index.yml 檔案中選擇的 JRE 版本。

```
'{repository_root: "https://locationToIndexYml", version: version-value}'
```
{: codeblock}

發出 `ibmcloud cf se myAPP` 指令來設定 **JBP_CONFIG_OPENJDK** 變數，例如：
```
ibmcloud cf se myApp JBP_CONFIG_OPENJDK '{repository_root: "https://myHostingApp.ng.bluemix.net", version: 1.8.+}'
```
{: codeblock}

*repository_root* URL 不會在 URL 中包括 `index.yml`。*repository_root* URL 會指向包含 `index.yml` 檔案的目錄層次，而不是檔案本身。

若要設定 JVM 環境變數，請發出下列指令：
```
ibmcloud cf se myApp JVM 'openjdk'
```
{: codeblock}

**附註**：請在設定環境變數之後，重新編譯打包應用程式，讓變更生效。

## 確認
{: #confirmation}

若要確認 Liberty 正在使用預期的 JRE，請檢查編譯打包日誌。請尋找一則訊息，指出伺服器已從 `index.yml` 檔案的位置下載建置套件。當 Liberty 順利使用預期的 JRE 時，請參閱下列 Snippet，以取得日誌輸出的範例。
```
   -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}
