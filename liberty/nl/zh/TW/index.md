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

{{site.data.keyword.Bluemix}} 上的 Liberty for Java 應用程式採用 liberty-for-java 建置套件的技術。除了 WebSphere Liberty 之外，liberty-for-java 建置套件還提供一個完整的運行環境來執行 Java EE 7 和 OSGi 應用程式。它支援例如 Spring 的熱門架構，且包含了 {{site.data.keyword.IBM_notm}} JRE。Liberty 讓您能進行極適合雲端的快速應用程式開發。
{: shortdesc}

## 偵測
{: #detection}
當部署下列類型的應用程式時，會使用 Liberty 建置套件：
* [WAR 檔](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)
* [EAR 檔](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)
* [Liberty 伺服器目錄](/docs/runtimes/liberty/optionsForPushing.html#server_directory)
* [Liberty 包裝伺服器](/docs/runtimes/liberty/optionsForPushing.html#packaged_server)
* Java main
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## 入門範本應用程式
{: #starter_application}
{{site.data.keyword.Bluemix_notm}} 提供數個 Liberty 入門範本應用程式。Liberty 入門範本應用程式是簡單的 Liberty 應用程式，提供可以讓您使用的範本。您可以使用入門範本應用程式進行實驗，並進行及推送對 {{site.data.keyword.Bluemix_notm}} 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](/docs/runtimes-common/starter_app_usage.html)。
