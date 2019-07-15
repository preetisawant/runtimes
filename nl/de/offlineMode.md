---

copyright:
  years: 2016, 2018
lastupdated: "2018-07-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Im Offlinemodus mit Node.js arbeiten
{: #offline_mode}

Wenn eine Node.js-Anwendung mit einer Push-Operation an {{site.data.keyword.Bluemix}} übertragen wird, lädt das Buildpack SDK for Node.js in der Regel Artefakte von externen Ressourcen herunter, z. B. Node-Module von NPM.  In einigen Situationen, beispielsweise mit [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) und
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), können Sie Zugriff auf Sites anpassen, die sich außerhalb von {{site.data.keyword.Bluemix_notm}} befinden.  
{: shortdesc}

Das Node.js-Buildpack kann auf die folgenden externen Sites zugreifen. Möglicherweise müssen Sie diese Sites in {{site.data.keyword.Bluemix_notm}}-Umgebungen des Typs [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) und
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) der *Whitelist* hinzufügen.

* http://nodejs.org/ kann verwendet werden, um verfügbare Knotenengine-Versionen zu ermitteln.
* https://s3pository.heroku.com wird verwendet, um Node-Engineversionen abzurufen, die im Buildpack nicht enthalten sind.
*  https://www.npmjs.com/package/npm und https://semver.herokuapp.com werden verwendet, um NPM-Versionen abzurufen, die im Buildpack nicht enthalten sind.
* https://iojs.org wird verwendet, um ältere Versionen des Knotens abzurufen, die entweder im Buildpack nicht enthalten oder unter https://semver.herokuapp.com nicht verfügbar sind.
* https://registry.npmjs.org wird verwendet, um Knotenmodule wie express abzurufen.

Konfigurieren Sie Ihre Anwendungen für die Verwendung einer Node-Engineversion, die im SDK for Node.js-Buildpack enthalten ist, um die Anzahl der Sites in der Whitelist zu reduzieren.  Die Gruppe der Node-Engineversionen, die im Buildpack enthalten ist, finden Sie in [Neueste Aktualisierungen](./updates.html).  Wenn Sie Ihre Anwendung so konfigurieren, dass diese Node-Engineversionen verwendet werden, ist nur die Site https://registry.npmjs.org erforderlich, um Module herunterzuladen.

Beachten Sie, dass sich bei der Installation von neuen Versionen des SDK for Node.js-Buildpacks die Gruppe der verfügbaren Engineversionen häufig zu neueren Versionen verschieben.  Eventuell müssen Sie Ihre App rekonfigurieren, um eine neuere Node-Engineversion anzugeben, die im Buildpack vorhanden ist.


## Offlineanwendungen
{: #offline_applications}

Damit nicht mehr auf https://registry.npmjs.org zugegriffen werden muss, können Sie alle Node-Module, die Ihre Anwendung benötigt, in die Anwendung einschließen.  Führen Sie dazu `npm install` für alle erforderlichen Anwendungsmodule aus und schließen Sie das resultierende Verzeichnis `node_modules` in die Anwendung ein, für die Sie die Push-Operation durchführen.

Ihre Abhängigkeiten können weitere Abhängigkeiten haben, die wiederum Abhängigkeiten haben usw. Die Datei `package.json` enthält jedoch nur die Abhängigkeiten der höchsten Ebene. Wenn eine Ihrer Abhängigkeiten einen Bereich in der Datei 'package.json' verwendet und hierzu eine neue Version freigegeben wird, können die Module dann in Ihrem Verzeichnis `node_modules` veraltet sein. *Shrinkwrap* unterstützt Sie, alle Abhängigkeitsversionen zu sperren, damit dies nicht auftritt.  Beginnen Sie mit einem leeren oder bereinigten Verzeichnis `node_modules`, um 'shrinkwrap' zu verwenden. Führen Sie anschließend im Stammverzeichnis Ihres Projekts die folgenden Befehle aus:

```
npm install
```
{: codeblock}

```
npm dedupe
```
{: codeblock}

```
npm shrinkwrap
```
{: codeblock}

Dadurch kann die Datei `package.json` geändert und `npm-shrinkwrap.json` zum Stammverzeichnis hinzugefügt werden.
Bei jeder Änderung der Abhängigkeiten in der Datei `package.json` müssen Sie die Befehle `npm dedupe` und `shrinkwrap` wiederholen.

## Mit einem Proxy arbeiten
{: #working_with_proxy}

In einigen Umgebungen, z. B. [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) und
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), kann ein Proxy konfiguriert werden. Weitere Informationen finden Sie unter [Mit einem Proxy arbeiten](/docs/manageapps/workingWithProxy.html).
