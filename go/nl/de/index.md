---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}

Die Laufzeit von Go in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'go_buildpack'.
Das Buildpack 'go_buildpack' bietet eine vollständige Laufzeitumgebung für Go-Apps.
{: shortdesc}

Das Buildpack 'go_buildpack' wird verwendet, wenn Ihre Anwendung eine Datei mit dem Namen '*.go' enthält.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} stellt eine Go-Starteranwendung bereit.  Die Go-Starteranwendung ist eine einfache Go-App, die Sie als Vorlage für Ihre App verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der {{site.data.keyword.Bluemix_notm}}-Umgebung vornehmen und diese mit einer Push-Operation übertragen. Informationen zur Verwendung der Starteranwendung finden Sie unter [Starteranwendungen verwenden](../common/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die Version von Go, die von Ihrer App verwendet werden soll, durch Festlegen der Eigenschaft 'GoVersion' in der Datei 'Godeps/Godeps.json' im Stammverzeichnis Ihrer Anwendung angeben. Beispiel:

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.10",
	"Deps": []
}
```
{: codeblock}
Weitere Informationen finden Sie in [godep](https://github.com/tools/godep){: new_window}.

Wenn keine Version angegeben ist, wird standardmäßig Version 1.8.7 ausgewählt.

### Verfügbare Versionen:
{: #available_versions}

Folgende Go-Versionen stehen im [Go-Buildpack](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.8.20){: new_window} zur Verfügung, das derzeit in {{site.data.keyword.Bluemix_notm}} installiert ist:

* 1.6.3
* 1.6.4
* 1.7.5
* 1.7.6
* 1.8.6
* 1.8.7
* 1.9.3
* 1.9.4
* 1.10

Wenn für Ihre App eine Go-Version erforderlich ist, die nicht aufgelistet ist, können Sie die Anwendung mit dem externen [Go-Buildpack](https://github.com/cloudfoundry/go-buildpack.git){: new_window} implementieren.

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}

* [GoLang](http://golang.org/){: new_window}
* [Cloud Foundry-Buildpack für Go](https://github.com/cloudfoundry/go-buildpack){: new_window}
