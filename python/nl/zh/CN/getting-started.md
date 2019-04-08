---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-05"
subcollection: "Python"


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
{: #getting_started}

* {: download}恭喜您，您已在 {{site.data.keyword.Bluemix}} 上部署了 Hello World 样本应用程序！要开始使用，请按照本逐步指南进行操作。或者，<a class="xref" href="http://bluemix.net" target="_blank" title="（下载样本代码）"><img class="hidden" src="../../images/btn_starter-code.svg" alt="下载应用程序代码" />下载样本代码</a>并自行探究。

按照 Python 入门教程，设置开发环境，在本地以及在 {{site.data.keyword.Bluemix}} 上部署应用程序，并在应用程序中集成数据库服务。

在这些文档中，对 Cloud Foundry CLI 的引用现已更新为 {{site.data.keyword.Bluemix_notm}} CLI！{{site.data.keyword.Bluemix_notm}} CLI 具有与 Cloud Foundry CLI 相同的常见命令，但它可以与 {{site.data.keyword.Bluemix_notm}} 帐户和其他服务更好地集成。在本教程中，可以了解有关如何使用 {{site.data.keyword.Bluemix_notm}} CLI 的更多信息。
{: tip}

## 开始之前
{: #prereqs}

您将需要以下内容：
* [{{site.data.keyword.Bluemix_notm}} 帐户](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/ibmcloud/download_cli.html)
* [Git ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://git-scm.com/downloads){: new_window}
* [Python ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.python.org/downloads/){: new_window}

## 步骤 1：克隆样本应用程序
{: #clone}

首先，克隆存储库，并切换到样本应用程序所在的目录。

  ```
git clone https://github.com/IBM-Cloud/get-started-python
  ```
  {: codeblock}

  ```
cd get-started-python
  ```
  {: codeblock}

仔细阅读 *get-started-python* 目录中的文件，以熟悉其内容。

## 步骤 2：本地运行应用程序
{: #run_locally}

请参阅 [The Hitchhiker’s Guide to Python! ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://docs.python-guide.org/en/latest/) 以帮助您在系统上设置 Python。
{: tip}

安装 [requirements.txt ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://pip.readthedocs.io/en/stable/user_guide/#requirements-files) 文件中列出的依赖项，以便能够在本地运行应用程序。

可以选择使用[虚拟环境 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://packaging.python.org/installing/#creating-and-using-virtual-environments)，以避免这些依赖项与其他 Python 项目或您操作系统中的依赖项发生冲突。


  ```
pip install -r requirements.txt
  ```
  {: codeblock}

若改用 Python3，可以发出

  ```
python3 -m pip install -r requirements.txt
  ```
  {: codeblock}

运行应用程序。
  ```
python hello.py
  ```
  {: codeblock}

 查看应用程序：http://localhost:8000


## 步骤 3：准备部署应用程序
{: #prepare}

如果要部署到 {{site.data.keyword.Bluemix_notm}}，设置 manifest.yml 文件会很有用。manifest.yml 包含有关应用程序的基本信息，例如名称、要为每个实例分配的内存量以及路径。我们在 `get-started-python` 目录中提供了样本 manifest.yml 文件。

打开 manifest.yml 文件，将 `name` 从 `GetStartedPython` 更改为您的应用程序名称 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>。
{: download}

  ```
  applications:
  - name: GetStartedPython
    random-route: true
    memory: 128M
  ```
  {: codeblock}

在此 manifest.yml 文件中，**random-route: true** 会为应用程序生成随机路径，以避免路径与其他路径冲突。如果您愿意，可以将 **random-route: true** 替换为 **host: myChosenHostName**，以提供您选择的主机名。
{: tip}

## 步骤 4：部署应用程序
{: #deploy}

可以使用 {{site.data.keyword.Bluemix_notm}} CLI 来部署应用程序。

1. 登录到 {{site.data.keyword.Bluemix_notm}} 帐户，然后选择 API 端点。

  ```
ibmcloud login
```
  {: codeblock}

  如果您有联合用户标识，请改用以下命令来使用单点登录标识进行登录。请参阅[使用联合标识登录](/docs/cli/login_federated_id.html)以了解更多信息。

  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. 设置目标 Cloud Foundry 组织和空间：

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  如果未设置组织或空间，请参阅[添加组织和空间](/docs/account/orgs_spaces.html)。
  {: tip}

1. 从 *get-started-python* 目录中，将应用程序推送到 {{site.data.keyword.Bluemix_notm}}

  ```
ibmcloud cf push
  ```
  {: codeblock}

  这可能需要一分钟。如果部署过程中发生错误，可以使用命令 `ibmcloud cf logs <Your-App-Name> --recent` 进行故障诊断。

部署完成后，应该会看到一条消息，指示应用程序正在运行。可以通过 push 命令输出中列出的 URL 查看应用程序。还可以发出以下命令来查看应用程序状态和 URL。

  ```
ibmcloud cf apps
```
  {: codeblock}

您还可以转至 {{site.data.keyword.Bluemix_notm}} [资源列表](https://cloud.ibm.com/resources)来查看应用程序。

## 步骤 5：添加数据库
{: #add_database}

接下来，我们要将 {{site.data.keyword.cloudant_short_notm}} NoSQL 数据库添加到此应用程序中，并设置此应用程序，使其可以在本地以及在 {{site.data.keyword.Bluemix_notm}} 上运行。

1. 在浏览器中，登录到 {{site.data.keyword.Bluemix_notm}}，然后转至“仪表板”。选择**创建资源**。
1. 搜索 **{{site.data.keyword.cloudant_short_notm}}**，并选择服务。
1. 针对**可用的认证方法**，选择**使用旧凭证和 IAM**。可以将其他字段保留缺省设置。单击**创建**来创建服务。
1. 在导航中，转至**连接**，然后单击**创建连接**。选择应用程序，并单击**连接**。
1. 使用缺省值，单击**连接并重新编译打包应用程序**以将数据库连接到应用程序。系统提示时，单击**重新编译打包**。

   {{site.data.keyword.Bluemix_notm}} 将重新启动应用程序，并使用 `VCAP_SERVICES` 环境变量为应用程序提供数据库凭证。此环境变量仅可用于在 {{site.data.keyword.Bluemix_notm}} 上运行的应用程序。

通过环境变量，可以将部署设置与源代码分开。例如，您可以将数据库密码存储在环境变量中，然后在源代码中引用此环境变量，而不是对密码进行硬编码。
{: tip}

## 步骤 6：使用数据库
{: #use_database}
现在，我们将更新本地代码以指向此数据库。我们将创建一个 JSON 文件，用于存储应用程序要使用的服务的凭证。仅当应用程序在本地运行时，才会使用此文件。在 {{site.data.keyword.Bluemix_notm}} 中运行时，将从 VCAP_SERVICES 环境变量中读取凭证。

1. 在 `get-started-python` 目录中，创建名为 `vcap-local.json` 的文件并包含以下内容：

  ```
{
  "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "username":"CLOUDANT_DATABASE_USERNAME",
            "password":"CLOUDANT_DATABASE_PASSWORD",
            "host":"CLOUDANT_DATABASE_HOST"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
  }
}
  ```
  {: codeblock}

2. 在 {{site.data.keyword.Bluemix_notm}} [资源列表](https://cloud.ibm.com/resources)中查找应用程序。在应用程序的“服务详细信息”页面上，单击侧边栏中的**连接**。单击 {{site.data.keyword.cloudant_short_notm}} 菜单图标 (**&hellip;**)，然后选择**查看凭证**。

3. 将凭证中的 `username`、`password` 和 `host` 复制并粘贴到 `vcap-local.json` 文件中的相同字段，以替换 **CLOUDANT_DATABASE_USERNAME**、**CLOUDANT_DATABASE_PASSWORD** 和 **CLOUDANT_DATABASE_URL**。

4. 在本地运行应用程序。

  ```
python hello.py
  ```
  {: codeblock}

查看应用程序：`http://localhost:8000`。现在，您输入到应用程序中的所有名称都已添加到数据库。

本地应用程序和 {{site.data.keyword.Bluemix_notm}} 应用程序共享该数据库。可以通过上面 push 命令输出中列出的 URL 查看 {{site.data.keyword.Bluemix_notm}} 应用程序。在刷新浏览器后，从任一应用程序添加的名称都应该会同时出现在这两个应用程序中。

请记住，如果无需应用程序继续运行，请将其停止，这样就不会产生任何意外的费用。
{: tip}

## 后续步骤

* [教程](/docs/tutorials/index.html)
* [样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
