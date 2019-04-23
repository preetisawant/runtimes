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

# 使用 IBM Eclipse Tools for {{site.data.keyword.cloud_notm}} 开发应用程序

还可以将 {{site.data.keyword.eclipsetoolsfull}} 用作开发应用程序并部署至 {{site.data.keyword.Bluemix}} 的替代方法。{{site.data.keyword.eclipsetoolsfull}} 提供了多个插件，可以安装到现有 Eclipse 环境中，以协助将您的集成开发环境 (IDE) 与 {{site.data.keyword.Bluemix_notm}} 相集成。

此过程遵循 Liberty [入门教程](getting-started.html)的相同常规步骤。使用 Eclipse，设置开发环境，在本地以及在云上部署应用程序，在应用程序中集成 {{site.data.keyword.Bluemix_notm}} 数据库服务。

## 开始之前
{: #prereqs}

您将需要以下帐户和工具：
* [IBM Eclipse Tools for IBM Cloud ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}
* [Eclipse IDE for Java EE Developers ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}

如果已完成[入门教程](getting-started.md)，那么可能已具有这些工具和帐户。在开始之前，确保您还安装了并注册了以下帐户：
* [{{site.data.keyword.Bluemix_notm}} 帐户](https://cloud.ibm.com/registration)
* [{{site.data.keyword.Bluemix_notm}} CLI](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://git-scm.com/downloads){: new_window}
* [Maven ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://maven.apache.org/download.cgi){: new_window}

## 步骤 1：克隆样本应用程序
{: #clone}

首先，克隆样本应用程序 GitHub 存储库。

  ```
git clone https://github.com/IBM-Cloud/get-started-java
  ```
  {: codeblock}

## 步骤 2：构建应用程序的源代码
{: #build_app}

使用 Maven 构建源代码，并运行生成的应用程序。

1. 在命令行上，切换到样本应用程序所在的目录。

  ```
cd get-started-java
  ```
  {: codeblock}

1. 使用 Maven 安装依赖项并构建 .war 文件。

  ```
mvn clean install
  ```
  {: codeblock}

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

在此 manifest.yml 文件中，**random-route: true** 会为应用程序生成随机路径，以避免路径与其他路径冲突。如果您愿意，可以将 **random-route: true** 替换为 **host: myChosenHostName**，以提供您选择的主机名。
{: tip}

## 步骤 4：登录到 {{site.data.keyword.Bluemix_notm}}
{: #deploy}

1. 登录到 {{site.data.keyword.Bluemix_notm}} 帐户，然后选择 API 端点。

  ```
ibmcloud login
```
  {: codeblock}

  如果由于您具有联合用户标识而无法使用 `ibmcloud login` 登录，请改用以下命令来使用单点登录标识进行登录。请参阅[使用联合标识登录](https://cloud.ibm.com/docs/iam?topic=iam-federated_id#federated_id)以了解更多信息。

  ```
ibmcloud login --sso
  ```
  {: codeblock}

  接下来，设置目标 Cloud Foundry CLI：

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  如果未设置组织或空间，请参阅[添加组织和空间](https://cloud.ibm.com/docs/account?topic=account-orgsspacesusers#orgsspacesusers)。
  {: tip}

## 步骤 5：使用 Eclipse 进行开发
{: #eclipse}

1. 确保您具有 [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix)。

2. 通过转至**文件 > 导入 > Maven > 现有 Maven 项目**，将 `get-started-java` 样本导入到 Eclipse。

3. 创建 Liberty 服务器定义。以下步骤将下载新的 Liberty 服务器。
  - 在**窗口 > 显示视图 > 服务器**视图中，右键单击并选择**新建 > 服务器**。
  - 选择 **IBM > WebSphere Application Server Liberty**。
  - 选择**通过归档或存储库安装**。
  - 出现提示时，输入要在其中安装 Liberty 的新文件夹的目标路径 (/Users/username/liberty)。
  - 选择**从 ibm.com 下载并安装新的运行时环境**。
  - 选择 **WAS Liberty with Java EE 7 Web Profile**。
  - 使用缺省选项继续执行向导，直到完成。

4. 在 Liberty 上本地运行应用程序：
  - 通过转至**窗口 > Web 浏览器 > 缺省系统 Web 浏览器**，将 Web 浏览器更改为系统缺省浏览器。
  - 右键单击 `GetStartedJava` 样本，并选择**运行方式 > 在服务器上运行**。
  - 找到并选择 localhost Liberty 服务器，然后单击**完成**。

  几秒后，应用程序将在以下地址运行：http://localhost:9080/GetStartedJava。

5. 更新代码：
  - 打开 `src/main/webapp/index.html`，然后将标题从 `<h1>Welcome.</h1>` 更新为 `<h1>Welcome Jane.</h1>`.
  - 保存更改。Liberty 将自动使更改生效。
  - 刷新浏览器 (http://localhost:9080/GetStartedJava) 以查看更改。

6. 将更改推送到 {{site.data.keyword.Bluemix_notm}}：
  - 在命令行的 `get-started-java` 目录中，重新构建 .war 文件。

    ```
mvn clean install
    ```
    {: codeblock}

  - 将应用程序推送到 {{site.data.keyword.Bluemix_notm}}。

    ```
ibmcloud cf push
    ```
    {: codeblock}

现在，您已在本地和云上运行代码！

## 步骤 6：添加数据库
{: #add_database}

接下来，我们要将 NoSQL 数据库添加到此应用程序并设置此应用程序，使其可以在本地以及在 {{site.data.keyword.Bluemix_notm}} 上运行。

1. 在浏览器中，登录到 {{site.data.keyword.Bluemix_notm}}，然后转至“仪表板”。选择**创建资源**。
2. 选择**数据和分析**部分，选择 **{{site.data.keyword.cloudant_short_notm}}**，然后创建该服务。
3. 转至**连接**视图，选择应用程序，然后选择**创建连接**。
4. 出现提示时，选择**重新编译打包**。{{site.data.keyword.Bluemix_notm}} 将重新启动应用程序，并使用 `VCAP_SERVICES` 环境变量为应用程序提供数据库凭证。此环境变量仅可用于在 {{site.data.keyword.Bluemix_notm}} 上运行的应用程序。

通过环境变量，可以将部署设置与源代码分开。例如，可以将数据库密码存储在环境变量中，然后在源代码中引用此环境变量，而不是对密码进行硬编码。
{: tip}

## 步骤 7：使用数据库
{: #use_database}
现在，我们将更新本地代码以指向此数据库。我们将在属性文件中存储服务的凭证。仅当应用程序在本地运行时，才会使用此文件。在 {{site.data.keyword.Bluemix_notm}} 中运行时，将从 `VCAP_SERVICES` 环境变量中读取凭证。

1. 在 Eclipse 中，打开 src/main/resources/cloudant.properties 文件：

  ```
  cloudant_url=
  ```
  {: codeblock}

2. 在浏览器中，转至 {{site.data.keyword.Bluemix_notm}} 并选择**应用程序 > _your app_ > 连接 > Cloudant > 查看凭证**。

3. 仅将凭证中的 `url` 复制并粘贴到 `cloudant.properties` 文件的 `url` 字段，然后保存更改。

  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:codeblock}

4. 在 Eclipse 中的`服务器`视图中，重新启动 Liberty 服务器。

  刷新浏览器视图：http://localhost:9080/GetStartedJava/。现在，您输入到应用程序中的所有名称都已添加到数据库。

  本地应用程序和 {{site.data.keyword.Bluemix_notm}} 应用程序共享该数据库。在刷新浏览器后，从任一应用程序添加的名称都将同时出现在这两个应用程序中。


请记住，如果无需应用程序在 {{site.data.keyword.Bluemix_notm}} 上继续运行，请停止该应用程序，这样就不会产生任何意外的费用。
{: tip}  
