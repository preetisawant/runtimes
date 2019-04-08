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

Le applicazioni Liberty for Java su {{site.data.keyword.Bluemix}} si avvalgono del pacchetto di build liberty-for-java. Il pacchetto di build liberty-for-java fornisce un ambiente di runtime completo per eseguire applicazioni Java EE 7 e OSGi su WebSphere Liberty. Supporta framework di uso comune come Spring e include {{site.data.keyword.IBM_notm}} JRE. Liberty abilita un rapido sviluppo delle applicazioni che è adatto per il cloud.
{: shortdesc}

## Rilevamento
{: #detection}
Il pacchetto di build Liberty viene utilizzato quando i seguenti tipi di applicazioni sono distribuiti:
* [File WAR](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)
* [File EAR](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)
* [Directory server Liberty](/docs/runtimes/liberty/optionsForPushing.html#server_directory)
* [Server in pacchetto Liberty](/docs/runtimes/liberty/optionsForPushing.html#packaged_server)
* Java principale
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## Applicazione starter
{: #starter_application}
{{site.data.keyword.Bluemix_notm}} fornisce diverse applicazioni starter Liberty.  Le applicazioni starter Liberty sono applicazioni Liberty semplici che forniscono un template che puoi utilizzare. Puoi fare delle prove con le applicazioni di avvio, apportare modifiche ed eseguirne il push
all'ambiente {{site.data.keyword.Bluemix_notm}}.  Consulta [Utilizzo di applicazioni starter](/docs/runtimes-common/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.
