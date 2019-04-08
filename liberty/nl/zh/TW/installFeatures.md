---

copyright:
  years: 2018
lastupdated: "2018-12-14"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# 安裝 Liberty 特性
{: #install-features}

Liberty for Java 運行環境包含 Liberty 所提供的[部分特性](libertyFeatures.html#liberty_features)。當應用程式推送至 {{site.data.keyword.cloud_notm}} 時，您可以執行 Liberty `installUtility` 指令，作為 Cloud Foundry 前置運行環境連結鉤，來安裝運行環境裡未包含的特性。

如需可用特性的完整清單，請參閱 [Liberty features ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)。

如需使用前置運行環境連結鉤的相關資訊，請參閱 Cloud Foundry 文件中的 [Configure Pre-Runtime Hooks ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.cloudfoundry.org/devguide/deploy-apps/deploy-app.html#profile)。

1. 在您要推送至 {{site.data.keyword.cloud_notm}} 的應用程式根目錄中，建立 `.profile.d` 目錄。

1. 在 `.profile.d` 目錄中，建立執行 `installUtility` 指令的 Script 檔，如下列範例中所示。

   此範例會安裝 `audit-1.0` 特性。

   ```
   #!/bin/sh
   echo "Installing audit-1.0"
   export PATH=$PATH:$HOME/.java/jre/bin

   $HOME/.liberty/bin/installUtility install audit-1.0 --acceptLicense
   ```
   {: codeblock}

   您可以指定其他特性名稱並以空格區隔，來安裝多個特性。
   {: tip}

1. 將您的應用程式推送至 {{site.data.keyword.cloud_notm}}，並使用 `-p` 參數來指定應用程式的根目錄。

   例如，執行下列指令來推送您的應用程式：
   ```
   ibmcloud cf push myApp -p /<path-to-application>
   ```
   {: codeblock}

1. 檢視應用程式的最近日誌來驗證特性已順利安裝。

   例如，執行下列指令來顯示日誌：
   ```
   ibmcloud cf logs myApp --recent
   ```
   {: codeblock}

    如果已安裝特性，輸出會顯示下列訊息：

    ```
    2018-09-18T13:01:17.61-0400 [APP/PROC/WEB/0] OUT Installing audit-1.0
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT Establishing a connection to the configured repositories ...
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT This process might take several minutes to complete.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Successfully connected to all configured repositories.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Preparing assets for installation. This process might take several minutes to complete.
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT The --acceptLicense argument was found. This indicates that you have
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT accepted the terms of the license agreement.
    ```
