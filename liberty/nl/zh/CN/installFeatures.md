---

copyright:
  years: 2018
lastupdated: "2018-10-03"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# 安装 Liberty 功能
{: #install-features}

Liberty for Java 运行时包含 Liberty 中可用的[功能子集](libertyFeatures.html#liberty_features)。可以通过运行 Liberty `installUtility` 命令来安装运行时中不包含的功能，作为将应用程序推送到 {{site.data.keyword.cloud_notm}} 时的 Cloud Foundry 运行前挂钩。

有关可用功能的完整列表，请参阅 [Liberty 功能部件![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)。

有关使用运行前挂钩的信息，请参阅 Cloud Foundry 文档中的 [Configure Pre-Runtime Hooks ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.cloudfoundry.org/devguide/deploy-apps/deploy-app.html#profile)。

1. 在要推送到 {{site.data.keyword.cloud_notm}} 的应用程序的根目录中，创建 `.profile.d` 目录。

1. 在 `.profile.d` 目录中，创建运行 `installUtility` 命令的脚本文件，如以下示例所示。

   此示例安装 `javaee-8.0` 功能。

   ```
   #!/bin/sh
   echo "Installing javaee-8.0"
   export PATH=$PATH:$HOME/.java/jre/bin

   $HOME/.liberty/bin/installUtility install javaee-8.0 --acceptLicense
   ```
   {: codeblock}

   可以通过指定空格分隔的其他功能名称来安装多个功能。
   {: tip}

1. 将应用程序推送到 {{site.data.keyword.cloud_notm}}，使用 `-p` 参数来指定应用程序的根目录。

   例如，运行以下命令来推送应用程序：
   ```
   ibmcloud cf push myApp -p /<path-to-application>
   ```
   {: codeblock}

1. 通过查看应用程序最近的日志，验证功能是否已安装成功。

   例如，运行以下命令来显示日志：
   ```
   ibmcloud cf logs myApp --recent
   ```
   {: codeblock}

    如果已安装功能，那么输出会显示以下消息：

    ```
    2018-09-18T13:01:17.61-0400 [APP/PROC/WEB/0] OUT Installing javaee-8.0
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT Establishing a connection to the configured repositories ...
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT This process might take several minutes to complete.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Successfully connected to all configured repositories.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Preparing assets for installation. This process might take several minutes to complete.
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT The --acceptLicense argument was found. This indicates that you have
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT accepted the terms of the license agreement.
    ```
