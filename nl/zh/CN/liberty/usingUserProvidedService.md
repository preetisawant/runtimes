---

copyright:
  years: 2017, 2018
lastupdated: "2018-6-26"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

#在 {{site.data.keyword.cloud_notm}} 中将用户提供的服务与 Liberty 配合使用
{: #using_user_provided}

Cloud Foundry 提供了一种机制，用于连接和使用不一定由 {{site.data.keyword.Bluemix_notm}} 环境提供或不一定在该环境中可用的服务。该功能即为[用户提供的服务](https://docs.cloudfoundry.org/devguide/services/user-provided.html)。

本文档假定：
  * 您有某个服务可用
  * 您可以获得该服务的凭证，并通过示例 Getting-Started-Liberty 样本应用程序描述连接和使用该服务所需的步骤

在本讨论中，我们将使用 CloudantNoSQLDB 实例作为示例服务，并创建一个用户提供的服务来连接该实例。

## 步骤 1：推送 Getting-Started 应用程序
{: #follow_getting_started}

执行[入门教程](/docs/runtimes/liberty/getting-started.html)中的步骤，一直执行到将应用程序推送到 {{site.data.keyword.Bluemix_notm}}。但在连接数据库之前停止。

## 步骤 2：创建 CloudantNoSQLDB 实例
{: #create_cloudantnosqldb}

执行[入门教程](/docs/runtimes/liberty/getting-started.html)中的步骤以创建 CloudantNoSQLDB 实例。

使用“查看凭证”选项从 CloudandNoSQLDB 中复制凭证。将这些凭证保存为本地文件，例如 cloudant-creds。

## 步骤 3：创建用户提供的服务
要使用 Getting-Started 应用程序，用户提供的服务的名称必须包含“cloudantNoSQLDB”。Getting-Started 应用程序将解析 VCAP 服务变量，并查找名称包含“cloudantNoSQLDB”的由用户提供的服务。

        ibmcloud cf cups my-cloudantNoSQLDB-ups -p cloudant-creds

## 步骤 4：绑定用户提供的服务并重新编译打包应用程序
将用户提供的服务绑定到 Getting-Started 应用程序。

        ibmcloud cf bs GettingStartedLiberty my-cloudantNoSQLDB-ups

        ibmcloud cf restage GettingStartedLiberty

## 步骤 5：确认
浏览至应用程序，并确认是否可以在“名称”字段中添加多个名称。
