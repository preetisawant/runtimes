---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-05"
subcollection: "Python"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}

Die Laufzeit von Python in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'python_buildpack'.
Das Buildpack 'python_buildpack' bietet eine vollständige Laufzeitumgebung für die Python-Apps 2 und 3.
{: shortdesc}

Das Buildpack 'python_buildpack' wird verwendet, wenn das Stammverzeichnis Ihrer App die Datei 'requirements.txt' oder die Datei 'setup.py' enthält.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} stellt eine Python-Starteranwendung bereit.  Die Python-Starteranwendung ist eine einfache Python-App, die Sie als Vorlage für Ihre App verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der {{site.data.keyword.Bluemix_notm}}-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starteranwendung finden Sie in [Starteranwendungen verwenden](docs/runtimes-common/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die Version von Python, die von Ihrer App verwendet werden soll, durch Festlegen von 'python-versionnumber' in der Datei 'runtime.txt' im Stammverzeichnis Ihrer Anwendung angeben. Beispiel:

```
python-3.6.4
```
{: codeblock}

Wenn keine Version angegeben ist, wird standardmäßig Version 2.7.14 ausgewählt.

### Verfügbare Versionen:
{: #available_versions}

Folgende Python-Versionen stehen im [Python-Buildpack](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.6.11) zur Verfügung, das zurzeit in {{site.data.keyword.Bluemix_notm}} installiert ist:

* 2.7.13
* 2.7.14
* 3.3.6
* 3.3.7
* 3.4.7
* 3.4.8
* 3.5.4
* 3.5.5
* 3.6.3
* 3.6.4

Wenn für Ihre Anwendung eine Python-Version erforderlich ist, die nicht aufgelistet ist, können Sie die App mit dem externen [Python-Buildpack](https://github.com/cloudfoundry/python-buildpack) implementieren.
