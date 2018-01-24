---

copyright:
  years: 2017
lastupdated: "2017-12-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# 入门教程

* {: download} 恭喜您，您已在 {{site.data.keyword.Bluemix}} 上部署了 Hello World 样本应用程序！要开始使用，请按照本逐步指南进行操作。或者，<a class="xref" href="http://bluemix.net" target="_blank" title="（下载样本代码）"><img class="hidden" src="../../images/btn_starter-code.svg" alt="下载应用程序代码" />下载样本代码</a>并自行探究。

按照 Liberty for Java 入门教程，设置开发环境，在本地以及在 {{site.data.keyword.Bluemix}} 上部署应用程序，并在应用程序中集成数据库服务。

## 在开始之前
{: #prereqs}

您将需要以下帐户和工具：
* [{{site.data.keyword.Bluemix_notm}} 帐户](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://git-scm.com/downloads){: new_window}
* [Maven ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://maven.apache.org/download.cgi){: new_window}

## 步骤 1：克隆样本应用程序
{: #clone}

首先，克隆样本应用程序 GitHub 存储库。
  ```bash
git clone https://github.com/IBM-Bluemix/get-started-java
  ```
  {: pre}


## 步骤 2: 使用命令行在本地运行应用程序
{: #run_locally}

使用 Maven 构建源代码，并运行生成的应用程序。

1. 在命令行上，切换到样本应用程序所在的目录。

  ```
cd get-started-java
  ```
  {: pre}

1. 使用 Maven 安装依赖项并构建 .war 文件。

  ```
mvn clean install
  ```
  {: pre}

1. 在 Liberty 上本地运行应用程序。
  ```
mvn install liberty:run-server
  ```
  {: pre}

看到消息 *The server defaultServer is ready to run a smarter planet.* 时，可以查看应用程序：http://localhost:9080/GetStartedJava。

要停止应用程序，请在启动该应用程序的命令行窗口中，按 *Ctrl-C*。

## 步骤 3：准备部署应用程序
{: #prepare}

如果要部署到 {{site.data.keyword.Bluemix_notm}}，设置 manifest.yml 文件会很有用。manifest.yml 包含有关应用程序的基本信息，例如名称、要为每个实例分配的内存量以及路径。我们在 `get-started-java` 目录中提供了样本 manifest.yml 文件。

打开 manifest.yml 文件，将 `name` 从 `GetStartedJava` 更改为您的应用程序名称 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>。
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

在此 manifest.yml 文件中，**random-route: true** 会为应用程序生成随机路径，以避免路径与其他路径冲突。如果您愿意，可以将 **random-route: true** 替换为 **host: myChosenHostName**，以提供您选择的主机名。[了解更多...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 步骤 4：部署到 {{site.data.keyword.Bluemix_notm}}
{: #deploy}

将应用程序部署到以下其中一个 {{site.data.keyword.Bluemix_notm}} 区域。为了获得最佳等待时间，请选择离您的用户最近的区域。

| **区域名称** | **地理位置** | **API 端点** |
|-----------------|-------------------------|-------------------|
| 美国南部区域 | 美国达拉斯 | api.ng.bluemix.net |
| 美国东部区域 | 美国华盛顿特区 | api.us-east.bluemix.net |
| 英国区域 | 英国伦敦 | api.eu-gb.bluemix.net |
| 悉尼区域 | 澳大利亚悉尼 | api.au-syd.bluemix.net |
| 德国区域 | 德国法兰克福 | api.eu-de.bluemix.net |
{: caption="表 1. {{site.data.keyword.cloud_notm}} 区域列表" caption-side="top"}

1. 设置 API 端点，方法是将 `<API-endpoint>` 替换为您区域的端点。
  ```
cf api <API-endpoint>
  ```
  {: pre}

1. 登录到 {{site.data.keyword.Bluemix_notm}} 帐户。
  ```
cf login
```
  {: pre}

  如果因为是联合用户标识而无法使用 `cf login` 或 `bx login` 命令登录，请使用 `cf login --sso` 或 `bx login --sso` 命令用单点登录标识登录。请参阅[使用联合标识登录](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id)以了解更多信息。


1. 从 `get-started-java` 目录中，将应用程序推送到 {{site.data.keyword.Bluemix_notm}}。
  ```
cf push
```
  {: pre}

部署应用程序可能需要几分钟时间。部署完成后，您将看到一条消息，指示应用程序正在运行。通过 push 命令输出中列出的 URL 查看应用程序，或者通过运行以下命令同时查看应用程序部署状态和 URL：
  ```
cf apps
  ```
  {: pre}

可以使用 `cf logs <Your-App-Name> --recent` 命令对部署过程中的错误进行故障诊断。
{: tip}  

## 步骤 5：添加数据库
{: #add_database}

接下来，我们要将 NoSQL 数据库添加到此应用程序并设置此应用程序，使其可以在本地以及在 {{site.data.keyword.Bluemix_notm}} 上运行。

1. 在浏览器中，登录到 {{site.data.keyword.Bluemix_notm}}，然后转至“仪表板”。通过在**名称**列中单击应用程序的名称以选择该应用程序。
2. 单击**连接**，然后单击**创建连接**。
3. 在**数据和分析**部分中，选择 **Cloudant NoSQL DB**，然后创建该服务。
4. 转至**应用程序 > your app > 连接**，然后选择**连接现有**。
5. 出现提示时，选择**重新编译打包**。{{site.data.keyword.Bluemix_notm}} 将重新启动应用程序，并使用 `VCAP_SERVICES` 环境变量为应用程序提供数据库凭证。此环境变量仅可用于在 {{site.data.keyword.Bluemix_notm}} 上运行的应用程序。

通过环境变量，可以将部署设置与源代码分开。例如，可以将数据库密码存储在环境变量中，然后在源代码中引用此环境变量，而不是对密码进行硬编码。[了解更多...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 步骤 7：使用数据库
{: #use_database}
现在，我们将更新本地代码以指向此数据库。我们将在属性文件中存储服务的凭证。仅当应用程序在本地运行时，才会使用此文件。在 {{site.data.keyword.Bluemix_notm}} 中运行时，将从 `VCAP_SERVICES` 环境变量中读取凭证。

1. 在浏览器中，转至 {{site.data.keyword.Bluemix_notm}} 并选择**应用程序 > _your app_ > 连接 > Cloudant > 查看凭证**。

2. 仅将凭证中的 `url` 复制并粘贴到 `cloudant.properties` 文件的 `url` 字段，然后保存更改。
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:pre}

3. 重新启动服务器

  刷新浏览器视图：http://localhost:9080/GetStartedJava/。现在，输入到应用程序中的所有名称都已添加到数据库。

  本地应用程序和 {{site.data.keyword.Bluemix_notm}} 应用程序共享该数据库。在刷新浏览器后，从任一应用程序添加的名称都将同时出现在这两个应用程序中。

请记住，如果无需应用程序在 {{site.data.keyword.Bluemix_notm}} 上继续运行，请停止该应用程序，这样就不会发生任何意外的费用。
{: tip}  

## 后续步骤

* [教程](/docs/tutorials/index.html)
* [样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
