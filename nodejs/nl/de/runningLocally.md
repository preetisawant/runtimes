---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Node.js-Anwendung lokal ausführen
{: #hints}

Legen Sie eine Portnummer fest, damit Sie Ihre Node.js-Anwendung lokal ausführen können, ohne dass Konflikte bei der Ausführung in {{site.data.keyword.Bluemix}} auftreten.
{: shortdesc}

Wenn die Anwendung in {{site.data.keyword.Bluemix_notm}} ausgeführt wird, wird die Umgebungsvariable PORT von Cloud Foundry zugeordnet. Bei lokaler Ausführung der Anwendung ist die Umgebungsvariablen PORT jedoch nicht definiert, sodass Sie den Port für Ihre Anwendung definieren können. Zum Vermeiden von Konflikten können Sie den Port, auf dem Ihre App lokal empfangsbereit ist, so definieren, dass er sich von dem von {{site.data.keyword.Bluemix_notm}} verwendeten Port etwas unterscheidet.

Im folgenden Beispiel für eine **js**-Datei wird **3000** als Portnummer verwendet. Bei der Verwendung von **3000** können Sie die Anwendung sowohl lokal für Testzwecke als auch in {{site.data.keyword.Bluemix_notm}} ausführen, ohne Änderungen vornehmen zu müssen.

```
var port = (process.env.PORT || 3000);
```
{: codeblock}
