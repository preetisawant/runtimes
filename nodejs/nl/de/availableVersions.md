---

copyright:
  years: 2015, 2017
lastupdated: "2017-06-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Verfügbare Versionen
{: #available_versions}

{{site.data.keyword.Bluemix}} stellt alle [aktuell verfügbaren Node.js-Laufzeiten](http://nodejs.org/dist/) bereit. Davon stellt IBM bestimmte Versionen zur Verfügung, die Erweiterungen und Fehlerkorrekturen enthalten. Weitere Informationen zu den unterstützten Versionen finden Sie in [Neueste Aktualisierungen für das Node.js-Buildpack](/docs/runtimes/nodejs/updates.html).
{: shortdesc}

Das IBM Node.js-Buildpack stellt die IBM Laufzeitversionen in den Cache. Wenn Sie die IBM SDK for Node.js-Laufzeit in Ihrer Anwendung verwenden, erzielen Sie eine bessere Anwendungsleistung, wenn die Anwendung mit einer Push-Operation an Bluemix übertragen wird.

## Version angeben

* Verwenden Sie den Parameter **node** im Abschnitt **engines** der Datei **package.json**, um die Version der Node.js-Laufzeit anzugeben, die Sie ausführen möchten.

* Wenn Sie eine andere als die mit Node.js im Paket vorhandene Version von npm angeben müssen, verwenden Sie den Parameter **npm** im Abschnitt **engines** der Datei **package.json**.  

Lesen Sie folgendes Beispiel:

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}

**Hinweis:** Für 'node' muss in der Datei **package.json** stets eine Version angegeben werden. Ist das nicht der Fall, wird die neueste Knotenversion verwendet.
