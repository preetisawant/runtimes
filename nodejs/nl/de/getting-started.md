---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-05"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}


# Lernprogramm 'Einführung'
{: #getting-started}

* {: download} Herzlichen Glückwunsch! Sie haben die Hello World-Beispielanwendung unter {{site.data.keyword.Bluemix}} bereitgestellt!  Befolgen Sie diese schrittweise Anleitung, um zu starten. Oder laden Sie den <a class="xref" href="http://bluemix.net" target="_blank" title="(Beispielcode herunterladen)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Anwendungscode herunterladen" />Beispielcode herunter</a> und beginnen Sie auf eigene Faust.

Indem Sie diesem Lernprogramm zur Einführung folgen, werden Sie eine Entwicklungsumgebung einrichten, eine App lokal und unter {{site.data.keyword.Bluemix}} bereitstellen und einen {{site.data.keyword.Bluemix_notm}}-Datenbankservice in Ihre App integrieren.

In diesen Dokumenten wurden Verweise auf die Cloud Foundry-Befehlszeilenschnittstelle (CLI) jetzt in Verweise auf die {{site.data.keyword.Bluemix_notm}}-CLI aktualisiert! Die {{site.data.keyword.Bluemix_notm}}-CLI besitzt die gleichen bekannten Cloud Foundry-Befehle, die jedoch besser in {{site.data.keyword.Bluemix_notm}}-Konten und andere Services integriert sind. Weitere Informationen zum Einstieg in die Arbeit mit der {{site.data.keyword.Bluemix_notm}}-CLI enthält dieses Lernprogramm.
{: tip}

## Vorbemerkungen
{: #prereqs}

Sie benötigen die folgenden Konten und Tools:
* [{{site.data.keyword.Bluemix_notm}}-Konto](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}}-CLI](/docs/cli/reference/ibmcloud/download_cli.html)
* [Git ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://git-scm.com/downloads){: new_window}
* [Node ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://nodejs.org/en/){: new_window}


## Schritt 1: Klonen Sie die Beispielapp.
{: #clone}

Klonen Sie zuerst die *hello world*-Beispielapp von Node.js 'GitHub repo'.
  ```
git clone https://github.com/IBM-Cloud/get-started-node
  ```
  {: codeblock}

## Schritt 2: Führen Sie die App lokal aus.
{: #run_locally}

Verwenden Sie den npm-Paketmanager, um Abhängigkeiten zu installieren und führen Sie Ihre App aus.

1. Wechseln Sie in der Befehlszeile in das Verzeichnis, in dem sich die Beispielapp befindet.
  ```
cd get-started-node
  ```
  {: codeblock}

1. Installieren Sie die Abhängigkeiten, die in der Datei [package.json ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.npmjs.com/files/package.json) aufgelistet sind, um die App lokal auszuführen.  
  ```
npm install
  ```
  {: codeblock}

1. Führen Sie die App aus.
  ```
npm start  
  ```
  {: codeblock}

1. Zeigen Sie Ihre App unter der folgenden URL an: http://localhost:3000

Verwenden Sie [nodemon](https://nodemon.io/) für den automatischen Neustart der Anwendung bei Dateiänderungen.
{: tip}

## Schritt 3: Bereiten Sie die App für die Bereitstellung vor.
{: #prepare}

Für die Bereitstellung unter {{site.data.keyword.Bluemix_notm}} kann es hilfreich sein, die Datei 'manifest.yml' zu installieren. Die Datei 'manifest.yml' enthält Basisinformationen zu Ihrer App wie den Namen, die Speichergröße, die für jede Instanz zugeordnet werden soll, und die Route. Eine Beispieldatei 'manifest.yml' wird im Verzeichnis `get-started-node` bereitgestellt.

Öffnen Sie die Datei 'manifest.yml' und ändern Sie die Angabe für `name` von `GetStartedNode` in den Namen Ihrer App <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

```
applications:
- name: GetStartedNode
  random-route: true
  memory: 128M
```
{: codeblock}

In dieser Datei 'manifest.yml' generiert **random-route: true** eine zufällige Route für Ihre App, um zu verhindern, dass Ihre Route mit anderen Routen kollidiert.  Wenn Sie möchten, können Sie **random-route: true** durch **host: myChosenHostName** ersetzen und einen Hostnamen Ihrer Wahl angeben.
{: tip}

## Schritt 4: Stellen Sie die App bereit.
{: #deploy}

Sie können die {{site.data.keyword.Bluemix_notm}}-CLI verwenden, um Apps in {{site.data.keyword.Bluemix_notm}} bereitzustellen.

1. Melden Sie sich an Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an und wählen Sie einen API-Endpunkt aus.
  ```
ibmcloud login
  ```
  {: codeblock}

  Wenn Sie eine eingebundene Benutzer-ID haben, verwenden Sie stattdessen den folgenden Befehl, um sich mit Ihrer Single Sign-on-ID anzumelden. Weitere Informationen finden Sie unter [Mit eingebundener ID anmelden](/docs/cli/login_federated_id.html#federated_id).
  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Legen Sie eine Cloud Foundry-Organisation und einen Bereich als Ziel fest:

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Wenn Sie keine eingerichtete Organisation oder keinen eingerichteten Bereich haben, finden Sie weitere Informationen unter [Organisationen und Bereiche hinzufügen](/docs/account/orgs_spaces.html).
    {: tip}

1. Übertragen Sie Ihre App mit einer Push-Operation aus dem Verzeichnis *get-started-node* zu {{site.data.keyword.Bluemix_notm}}.

  ```
ibmcloud cf push
  ```
  {: codeblock}

Das Bereitstellen Ihrer Anwendung kann einige Minuten dauern. Wenn die Bereitstellung abgeschlossen ist, sehen Sie eine Nachricht darüber, dass Ihre App ausgeführt wird. Ihre App wird unter der URL angezeigt, die in der Ausgabe des Push-Befehls aufgelistet ist. Sie können aber auch den App-Bereitstellungsstatus und die URL anzeigen, indem Sie folgenden Befehl ausführen:

  ```
ibmcloud cf apps
  ```
  {: codeblock}

Sie können die App auch über die {{site.data.keyword.Bluemix_notm}} [Ressourcenliste](https://cloud.ibm.com/resources) anzeigen. 

Sie können nach Fehlern im Bereitstellungsprozess suchen, indem Sie den Befehl `ibmcloud cf logs <Your-App-Name> --recent` verwenden.
{: tip}

## Schritt 5: Fügen Sie eine Datenbank hinzu.
{: #add_database}

Als Nächstes werden Sie dieser Anwendung eine {{site.data.keyword.cloudant_short_notm}} NoSQL-Datenbank hinzufügen und die Anwendung so einrichten, dass sie lokal und unter {{site.data.keyword.Bluemix_notm}} ausgeführt werden kann.

1. Melden Sie sich in Ihrem Browser bei {{site.data.keyword.Bluemix_notm}} an und wechseln Sie zum Dashboard. Wählen Sie **Ressource erstellen** aus.
1. Suchen Sie nach **{{site.data.keyword.cloudant_short_notm}}** und wählen Sie den Service aus.
1. Wählen Sie für **Verfügbare Authentifizierungsmethoden** die Option **Sowohl traditionelle Berechtigungsnachweise als auch IAM verwenden** aus. Sie können die Standardeinstellungen für die anderen Felder belassen. Klicken Sie auf **Erstellen**, um den Service zu erstellen.
1. Rufen Sie in der Navigation **Verbindungen** auf und klicken Sie dann auf **Verbindung erstellen**. Wählen Sie Ihre Anwendung aus und klicken Sie auf **Verbinden**. 
1. Verwenden Sie die Standardwerte und klicken Sie auf **Verbinden & Erneutes Staging für App**, um eine Verbindung von der Datenbank zur Anwendung herzustellen. Klicken Sie auf **Erneutes Staging**, wenn Sie dazu aufgefordert werden. 

   {{site.data.keyword.Bluemix_notm}} startet Ihre Anwendung erneut und stellt die Datenbankberechtigungsnachweise für Ihre Anwendung durch die Umgebungsvariable `VCAP_SERVICES` bereit. Diese Umgebungsvariable ist nur dann für die Anwendung verfügbar, wenn sie unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Umgebungsvariablen ermöglichen es Ihnen, die Bereitstellungseinstellungen von Ihrem Quellcode zu trennen. Beispiel: Anstelle der festen Codierung eines Datenbankkennworts können Sie es in einer Umgebungsvariablen speichern, auf die Sie in Ihrem Quellcode verweisen.
{: tip}

## Schritt 6: Verwenden Sie die Datenbank.
{: #use_database}
Sie werden jetzt Ihren lokalen Code aktualisieren, um auf diese Datenbank zu verweisen. Sie erstellen nun eine JSON-Datei, in der die Berechtigungsnachweise für die Services gespeichert werden, die die Anwendung verwenden soll. Diese Datei wird NUR dann verwendet, wenn die Anwendung lokal ausgeführt wird. Bei der Ausführung in {{site.data.keyword.Bluemix_notm}} werden die Berechtigungsnachweise aus der Umgebungsvariablen `VCAP_SERVICES` gelesen.

1. Erstellen Sie im Verzeichnis `get-started-node` eine Datei mit dem Namen `vcap-local.json` mit dem folgenden Inhalt:
  ```
  {
    "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "url":"CLOUDANT_DATABASE_URL"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
    }
  }
  ```
  {: codeblock}

2. Suchen Sie Ihre App in der {{site.data.keyword.Bluemix_notm}} [Ressourcenliste](https://cloud.ibm.com/resources). Klicken Sie auf der Servicedetailseite für die App auf **Verbindungen** in der Seitenleiste. Klicken Sie auf das {{site.data.keyword.cloudant_short_notm}}-Menüsymbol (**&hellip;**) und wählen Sie **Berechtigungsnachweise anzeigen** aus.

3. Kopieren Sie einfach die `url` aus den Berechtigungsnachweisen in das Feld `url` der Datei `vcap-local.json` und ersetzen Sie dabei `CLOUDANT_DATABASE_URL`.

4. Führen Sie Ihre Anwendung lokal aus.
  ```
npm start  
  ```
  {: codeblock}

  Ihre lokale App finden Sie unter http://localhost:3000. Alle Namen, die Sie in die App eingegeben haben, werden der Datenbank jetzt hinzugefügt.

**Probleme vermeiden**: {{site.data.keyword.Bluemix_notm}} definiert die Umgebungsvariable PORT, wenn Sie Ihre App in der Cloud ausführen. Wenn Sie Ihre App lokal ausführen, wird die Variable PORT nicht definiert, sodass 3000 als Portnummer verwendet wird. Weitere Informationen finden Sie in [App lokal ausführen](runningLocally.html#hints).

  Ihre lokale App und die {{site.data.keyword.Bluemix_notm}}-App verwenden die Datenbank gemeinsam. Namen, die Sie in einer der Apps eingeben, werden nach einer Aktualisierung des Browsers in beiden angezeigt.

Denken Sie daran, dass Sie Ihre App unter {{site.data.keyword.Bluemix_notm}} stoppen, wenn Sie sie nicht benötigen, damit keine unerwarteten Gebühren anfallen.
{: tip}

## Nächste Schritte

* [Lernprogramme](/docs/tutorials/index.html)
* [Beispiele ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
