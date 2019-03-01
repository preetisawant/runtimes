---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

Die Liberty for Java-Anwendungen in {{site.data.keyword.Bluemix}} basieren auf dem Buildpack 'liberty-for-java'. Mit dem Buildpack 'liberty-for-java' wird eine vollständige Laufzeitumgebung zum Ausführen von Java EE 7- und OSGi-Anwendungen auf Basis von WebSphere Liberty bereitgestellt. Es unterstützt gängige Frameworks wie Spring und umfasst die {{site.data.keyword.IBM_notm}} JRE. Liberty ermöglicht eine zeiteffiziente Anwendungsentwicklung, die gut auf die Cloud abgestimmt ist.
{: shortdesc}

## Erkennung
{: #detection}
Das Liberty-Buildpack wird verwendet, wenn folgende Anwendungsarten bereitgestellt werden:
* [WAR-Dateien](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)
* [EAR-Dateien](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)
* [Liberty-Serververzeichnis](/docs/runtimes/liberty/optionsForPushing.html#server_directory)
* [Paketierter Liberty-Server](/docs/runtimes/liberty/optionsForPushing.html#packaged_server)
* Main-Methode von Java
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## Starteranwendung
{: #starter_application}
{{site.data.keyword.Bluemix_notm}} stellt mehrere Liberty-Starteranwendungen bereit.  Die Liberty-Starteranwendungen sind einfache Liberty-Apps, die Sie als Vorlage verwenden können. Sie können mit den Starter-Apps experimentieren, Änderungen an der {{site.data.keyword.Bluemix_notm}}-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starteranwendungen finden Sie in [Starteranwendungen verwenden](/docs/runtimes-common/starter_app_usage.html).
