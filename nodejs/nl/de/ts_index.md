---

copyright:
  years: 2017
lastupdated: "2017-12-15"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# SDK for Node.js - Fehlerbehebung
{: #ts}


Es folgen die Antworten auf allgemeine Fragen zur Fehlerbehebung bei der Verwendung von SDK for Node.js in {{site.data.keyword.Bluemix}}.
{:shortdesc}

Weitere Informationen zu Protokollierung und Tracing finden Sie im Abschnitt [Trace](../../manageapps/app_mng.html#trace) in [Liberty- und Node.js-Anwendungen verwalten](../../manageapps/app_mng.html).

## Das Starten der Anwendung schlug mit der Nachricht über fehlenden Speicherplatz auf der Einheit fehl: “No space left on device”.
{: #no_space_left_on_device}


Das Starten einer Node.js-Anwendung schlug mit der Nachricht “No space left on device” fehl. Der Fehler kann in den Protokollen beispielsweise wie folgt aussehen:
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

Node.js-Anwendungen, die NPM-Versionen vor Version 3 verwenden, verbrauchen mehr Speicherplatz beim Herunterladen von Abhängigkeiten.
{: tsCauses}

Ändern Sie die Datei 'package.json' für Ihre Anwendung, um eine NPM-Version zu verwenden, die höher als Version 3 ist.
{: tsResolve}

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

## Anwendung wird aufgrund von Speicherengpass neu gestartet
{: #oom}

Node.js ist nicht bekannt, wie viel Speicher der Anwendung zur Verfügung steht. Der Garbage-Collector wird daher möglicherweise erst ausgeführt, wenn der Speicherplatz ausgeschöpft ist.

```
2017-09-01T11:00:42.19-0400 [APP/PROC/WEB/0]OUT Exit status 137
2017-09-01T11:00:42.23-0400 [CELL/0]     OUT Exit status 0
2017-09-01T11:00:42.27-0400 [CELL/0]     OUT Destroying container
2017-09-01T11:00:42.34-0400 [API/0]      OUT Process has crashed with type: "web"
2017-09-01T11:00:42.36-0400 [API/0]      OUT App instance exited with guid eecfba3b-430c-4a6b-b71f-ac72816fe152 payload: {"instance"=>"77dbb981-16d0-3a05-3235-9a4b", "index"=>0, "reason"=>"CRASHED", "exit_description"=>"2 error(s) occurred:\n\n* 2 error(s) occurred:\n\n* Exited with status 137 (out of memory)\n* cancelled\n* cancelled", "crash_count"=>1, "crash_timestamp"=>1504278042244633291, "version"=>"6497b5b5-67d4-4c5a-b1af-362e522a029d"}
2017-09-01T11:00:43.35-0400 [CELL/0]     OUT Successfully destroyed container
```
{: codeblock}

Eine mögliche Lösung ist das Festlegen der Option `--max_old_space_size` für den Startbefehl der Anwendung in der package.json-Datei. Diese Option stellt einen Teil des Speicherbedarfs der Anwendung dar. Sie sollte auf einen Wert gesetzt werden, der unter dem Wert des für die Anwendung verfügbaren Gesamtspeichers liegt. Eine detailliertere Beschreibung zu diesem Thema finden Sie im Abschnitt über große Speicherlastspitzen auf Heroku [(Large memory spikes on Heroku)](https://github.com/nodejs/node/issues/3370).
```
  "scripts": {
    "start": "node --max_old_space_size=800 server.js"
  }
```
{: codeblock}
