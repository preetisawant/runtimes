---

copyright:
  years: 2018
lastupdated: "2018-12-14"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# Liberty フィーチャーのインストール
{: #install-features}

Liberty for Java ランタイムには、Liberty で使用可能な[フィーチャーのサブセット](libertyFeatures.html#liberty_features)が含まれています。 アプリケーションが {{site.data.keyword.cloud_notm}} にプッシュされるときに Cloud Foundry のランタイム前のフックとして Liberty `installUtility` コマンドを実行することによって、ランタイムに含まれていないフィーチャーをインストールできます。

使用可能なフィーチャーの完全なリストについては、[Liberty フィーチャー ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html) を参照してください。

ランタイム前フックの使用について詳しくは、Cloud Foundry 資料で [Configure Pre-Runtime Hooks ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.cloudfoundry.org/devguide/deploy-apps/deploy-app.html#profile) を参照してください。

1. {{site.data.keyword.cloud_notm}} にプッシュしたいアプリケーションのルート・ディレクトリーに、`.profile.d` ディレクトリーを作成します。

1. `.profile.d` ディレクトリーに、以下の例のように `installUtility` コマンドを実行するスクリプト・ファイルを作成します。

   この例は、`audit-1.0` フィーチャーをインストールします。

   ```
   #!/bin/sh
   echo "Installing audit-1.0"
   export PATH=$PATH:$HOME/.java/jre/bin

   $HOME/.liberty/bin/installUtility install audit-1.0 --acceptLicense
   ```
   {: codeblock}

   追加のフィーチャー名をスペースで区切って指定することによって、複数のフィーチャーをインストールできます。
   {: tip}

1. `-p` パラメーターを使用してアプリケーションのルート・ディレクトリーを指定して、{{site.data.keyword.cloud_notm}} にアプリケーションをプッシュします。

   例えば、以下のコマンドを実行してアプリケーションをプッシュします。
   ```
   ibmcloud cf push myApp -p /<path-to-application>
   ```
   {: codeblock}

1. アプリケーションの最近のログを確認して、フィーチャーが正常にインストールされたことを検証します。

   例えば、以下のコマンドを実行してログを表示します。
   ```
   ibmcloud cf logs myApp --recent
   ```
   {: codeblock}

    フィーチャーがインストールされた場合、次のメッセージが出力されます。

    ```
    2018-09-18T13:01:17.61-0400 [APP/PROC/WEB/0] OUT Installing audit-1.0
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT Establishing a connection to the configured repositories ...
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT This process might take several minutes to complete.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Successfully connected to all configured repositories.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Preparing assets for installation. This process might take several minutes to complete.
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT The --acceptLicense argument was found. This indicates that you have
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT accepted the terms of the license agreement.
    ```
