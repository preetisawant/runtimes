---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"
subcollection: "liberty"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

{{site.data.keyword.Bluemix}} 上的 Liberty for Java 应用程序由 liberty-for-java buildpack 提供技术支持。liberty-for-java buildpack 提供了在 WebSphere Liberty 之上运行 Java EE 7 和 OSGi 应用程序所需的完整运行时环境。它支持 Spring 等流行框架，并包含 {{site.data.keyword.IBM_notm}} JRE。Liberty 支持快速应用程序开发，这非常适合云环境。
{: shortdesc}

## 检测
{: #detection}
部署以下类型的应用程序时，将使用 Liberty buildpack：
* [WAR 文件](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)
* [EAR 文件](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)
* [Liberty 服务器目录](/docs/runtimes/liberty/optionsForPushing.html#server_directory)
* [Liberty 打包服务器](/docs/runtimes/liberty/optionsForPushing.html#packaged_server)
* Java main
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## 入门模板应用程序
{: #starter_application}
{{site.data.keyword.Bluemix_notm}} 提供了几种 Liberty 入门模板应用程序。Liberty 入门模板应用程序是为您提供可使用模板的简单 Liberty 应用程序。您可以尝试使用入门模板应用程序来进行更改并将更改推送到 {{site.data.keyword.Bluemix_notm}} 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](/docs/runtimes-common/starter_app_usage.html)。
