---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Node.js
{: #nodejs_runtime}

Il runtime Node.js su {{site.data.keyword.Bluemix}} si avvale della tecnologia del pacchetto di build sdk-for-nodejs.
Il pacchetto di build sdk-for-nodejs fornisce un ambiente di runtime completo per le applicazioni Node.js.
{: shortdesc}

Il pacchetto di build sdk-for-nodejs è utilizzato quando l'applicazione contiene un file **package.json** nella directory root.

L'applicazione deve essere in ascolto sulla porta assegnata ad essa tramite la variabile di ambiente PORT.
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} Fornisce un'applicazione starter Node.js.  L'applicazione starter Node.js è un'applicazione Node.js semplice che fornisce un template che puoi utilizzare per la tua applicazione. Puoi sperimentare l'applicazione starter ed effettuare e inviare modifiche all'ambiente {{site.data.keyword.Bluemix_notm}} Consulta [Utilizzo di applicazioni starter](/docs/runtimes-common/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

## Gestione applicazioni
{: #app_management}
{{site.data.keyword.Bluemix_notm}} fornisce diversi programmi di utilità per la gestione e il debug della tua applicazione Node.js.  Consulta [Gestione applicazioni](/docs/runtimes-common/app_mng.html) per i dettagli completi.
