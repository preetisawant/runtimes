---

copyright:
  years: 2016, 2018
lastupdated: "2018-11-20"
subcollection: "liberty"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Offlinemodus für Liberty verwenden
{: #offline_mode}

Wenn eine Liberty-Anwendung mit einer Push-Operation an {{site.data.keyword.Bluemix}} übertragen wird,
kann das Liberty-Buildpack auf externe Sites in {{site.data.keyword.Bluemix_notm}} zugreifen, um von der Anwendung benötigte Artefakte anzufordern.  Das Liberty-Buildpack kann auf folgende externe Sites zugreifen.  In den Umgebungen [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) und
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) müssen diese Sites ggf. *in einer Whitelist aufgeführt* sein.

* https://download.run.pivotal.io und https://java-buildpack.cloudfoundry.org werden verwendet, um auf Komponenten zuzugreifen für:
  * [AppDynamics-Agent ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.appdynamics.com/)
  * [MariaDB JDBC-Treiber ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mariadb.com/)
  * [New Relic-Agent](/docs/runtimes/liberty/monitoring/newRelic.html)
  * [OpenJDK](/docs/runtimes/liberty/customizingJRE.html#OpenJDK)
  * [PostgreSQL JDBC-Treiber ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ wird verwendet, um auf Komponenten für [JRebel ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://zeroturnaround.com/software/jrebel/) zuzugreifen.
* https://download.ruxit.com/agent/paas/cloudfoundry/java wird verwendet, um auf Komponenten für den [Dynatrace Ruxit-Agenten](dynatrace.html) zuzugreifen.
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/ wird verwendet, um auf den [Dynatrace-Agenten](dynatrace.html) zuzugreifen.

## Mit einem Proxy arbeiten
{: #working_with_proxy}

In einigen Umgebungen, z. B. [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) und
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), kann ein Proxy konfiguriert werden. Weitere Informationen finden Sie unter [Mit einem Proxy arbeiten](/docs/runtimes-common/workingWithProxy.html).
