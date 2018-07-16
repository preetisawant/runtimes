---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

Le applicazioni Liberty for Java su {{site.data.keyword.Bluemix}} si avvalgono del pacchetto di build liberty-for-java. Il pacchetto di build liberty-for-java fornisce un ambiente di runtime completo per eseguire applicazioni Java EE 7 e OSGi su WebSphere Liberty. Supporta framework di uso comune come Spring e include {{site.data.keyword.IBM_notm}} JRE. Liberty abilita un rapido sviluppo delle applicazioni che è adatto per il cloud.
{: shortdesc}

## Rilevamento
{: #detection}
Il pacchetto di build Liberty viene utilizzato quando i seguenti tipi di applicazioni sono distribuiti:
* [File WAR](optionsForPushing.html#stand_alone_apps)
* [File EAR](optionsForPushing.html#stand_alone_apps)
* [Directory server Liberty](optionsForPushing.html#server_directory)
* [Server in pacchetto Liberty](optionsForPushing.html#packaged_server)
* Java principale
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## Applicazione starter
{: #starter_application}
{{site.data.keyword.Bluemix_notm}} fornisce diverse applicazioni starter Liberty.  Le applicazioni starter Liberty sono applicazioni Liberty semplici che forniscono un template che puoi utilizzare. Puoi fare delle prove con le applicazioni di avvio, apportare modifiche ed eseguirne il push
all'ambiente {{site.data.keyword.Bluemix_notm}}.  Consulta [Utilizzo di applicazioni starter](../common/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [Gestione delle applicazioni Liberty](../common/app_mng.html#Utilities)
* [Distribuzione di applicazioni con IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [Introduzione a {{site.data.keyword.loganalysislong_notm}}](/docs/services/CloudLogAnalysis/index.html)
* [Introduzione a {{site.data.keyword.prf_hublong}}](/docs/services/AvailabilityMonitoring/index.html)
