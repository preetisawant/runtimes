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

Die Laufzeit von Node.js in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'sdk-for-nodejs'.
Das Buildpack 'sdk-for-nodejs' bietet eine vollständige Laufzeitumgebung für Node.js-Apps.
{: shortdesc}

Das Buildpack 'sdk-for-nodejs' wird verwendet, wenn die Anwendung die Datei **package.json** im Stammverzeichnis enthält.

Die Anwendung muss auf dem Port empfangsbereit sein, der ihr über die Umgebungsvariable PORT zugeordnet ist.
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} stellt eine Node.js-Starteranwendung bereit. Die Node.js-Starteranwendung ist eine einfache Node.js-App, die Sie als Vorlage für Ihre App verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der {{site.data.keyword.Bluemix_notm}}-Umgebung vornehmen und diese mit einer Push-Operation übertragen. Informationen zur Verwendung der Starteranwendung finden Sie unter [Starteranwendungen verwenden](../common/starter_app_usage.html).

## App-Management
{: #app_management}
{{site.data.keyword.Bluemix_notm}} stellt eine Anzahl Dienstprogramme für das Management und das Debugging Ihrer Node.js-App zur Verfügung.  Vollständige Details finden Sie in [App-Management](../common/app_mng.html).

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Node.js ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://nodejs.org)
* [IBM API Connect](https://strongloop.com/)
