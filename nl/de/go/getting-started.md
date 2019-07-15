---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-03"

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

* {: download} Herzlichen Glückwunsch! Sie haben die Hello World-Beispielanwendung unter {{site.data.keyword.Bluemix}} bereitgestellt!  Befolgen Sie diese schrittweise Anleitung, um zu starten. Oder laden Sie den <a class="xref" href="http://bluemix.net" target="_blank" title="(Beispielcode herunterladen)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Anwendungscode herunterladen" />Beispielcode herunter</a> und beginnen Sie auf eigene Faust.

Indem Sie diesem Lernprogramm zur Einführung folgen, werden Sie eine Entwicklungsumgebung einrichten, eine App lokal und unter {{site.data.keyword.Bluemix}} bereitstellen und einen {{site.data.keyword.Bluemix_notm}}-Datenbankservice in Ihre App integrieren.

In diesen Dokumenten wurden Verweise auf die Cloud Foundry-Befehlszeilenschnittstelle (CLI) jetzt in Verweise auf die {{site.data.keyword.Bluemix_notm}}-CLI aktualisiert! Die {{site.data.keyword.Bluemix_notm}}-CLI besitzt die gleichen bekannten Cloud Foundry-Befehle, die jedoch besser in {{site.data.keyword.Bluemix_notm}}-Konten und andere Services integriert sind. Weitere Informationen zum Einstieg in die Arbeit mit der {{site.data.keyword.Bluemix_notm}}-CLI enthält dieses Lernprogramm.
{: tip}

## Vorbemerkungen
{: #prereqs}

Sie benötigen Folgendes:
* [{{site.data.keyword.Bluemix_notm}}-Konto](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}}-CLI](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://git-scm.com/downloads){: new_window}
* [Go ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://golang.org/dl/){: new_window}

## Schritt 1: Klonen Sie die Beispielapp.
{: #clone}

1. Zuerst richten Sie die lokale Umgebung ein, indem Sie sicherstellen, dass alle GO-Umgebungsvariablen ordnungsgemäß definiert werden. Beispiel:

  ```
mkdir $HOME/work
export GOPATH=$HOME/work
export PATH=$PATH:$GOPATH/bin
  ```
  {: codeblock}

1. Ändern Sie den Pfad in $GOPATH/src.

  ```
mkdir $GOPATH/src
cd $GOPATH/src
  ```
  {: codeblock}

  Jetzt können Sie beginnen, mit der einfachen Go-App *hello world* zu arbeiten.
1. Klonen Sie das Repository und wechseln Sie in das Verzeichnis, in dem sich die Beispielapp befindet.

  ```
go get github.com/IBM-Cloud/get-started-go
  ```
  {: codeblock}

  ```
cd github.com/IBM-Cloud/get-started-go
  ```
  {: codeblock}

1. Lesen Sie die Dateien im Verzeichnis **`get-started-go`**, um sich mit deren Inhalt vertraut zu machen.

## Schritt 2: Führen Sie die App lokal aus.
{: #run_locally}

1. Erstellen Sie einen Build der App und führen Sie die App lokal aus, indem Sie die folgenden Befehle ausführen.

  ```
make
  ```
  {: codeblock}

  ```
go run main.go
  ```
  {: pre}

1. Zeigen Sie Ihre App unter der folgenden URL an: http://localhost:8080

Drücken Sie in dem Fenster, in dem Sie Ihre App gestartet haben, die Tastenkombination *Strg-C*, um die App zu stoppen.
{: tip}

## Schritt 3: Bereiten Sie die App für die Bereitstellung vor.
{: #prepare}

Für die Bereitstellung unter {{site.data.keyword.Bluemix_notm}} kann es hilfreich sein, die Datei 'manifest.yml' zu installieren. Die Datei 'manifest.yml' enthält Basisinformationen zu Ihrer App wie den Namen, die Speichergröße, die für jede Instanz zugeordnet werden soll, und die Route. Eine Beispieldatei 'manifest.yml' wird im Verzeichnis `get-started-go` bereitgestellt.

Öffnen Sie die Datei 'manifest.yml' und ändern Sie die Angabe für `name` von `GetStartedGo` in den Namen Ihrer App <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedGo
   random-route: true
   memory: 128M
   buildpack: go_buildpack
  ```
  {: codeblock}

In dieser Datei 'manifest.yml' generiert **`random-route: true`** eine zufällige Route für Ihre App, um zu verhindern, dass Ihre Route mit anderen Routen kollidiert.  Wenn Sie möchten, können Sie **`random-route: true`** durch **`host: myChosenHostName`** ersetzen und einen Hostnamen Ihrer Wahl angeben.
{: tip}

## Schritt 4: Stellen Sie die App bereit.
{: #deploy}

Sie können Apps über die {{site.data.keyword.Bluemix_notm}}-CLI bereitstellen.

1. Melden Sie sich an Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an und wählen Sie einen API-Endpunkt aus.

  ```
ibmcloud login
  ```
  {: codeblock}

  Wenn Sie eine eingebundene Benutzer-ID haben, verwenden Sie stattdessen den folgenden Befehl, um sich mit Ihrer Single Sign-on-ID anzumelden. Weitere Informationen finden Sie unter [Mit eingebundener ID anmelden](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id).

  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Legen Sie eine Cloud Foundry-Organisation und einen Bereich als Ziel fest:

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Wenn Sie keine eingerichtete Organisation oder keinen eingerichteten Bereich haben, finden Sie weitere Informationen unter [Organisationen und Bereiche hinzufügen](https://console.bluemix.net/docs/account/orgs_spaces.html).
  {: tip}

1. Übertragen Sie Ihre App mit einer Push-Operation aus dem Verzeichnis **`get-started-go`** an {{site.data.keyword.Bluemix_notm}}.

  ```
ibmcloud cf push
  ```
  {: codeblock}

  Dieser Vorgang kann einige Minuten dauern. Falls ein Fehler im Bereitstellungsprozess auftritt, können Sie mithilfe des Befehls `ibmcloud cf logs <Your-App-Name> --recent` nach dem Fehler suchen.

Wenn die Bereitstellung abgeschlossen ist, sollte eine Nachricht anzeigen, dass Ihre App ausgeführt wird.  Ihre App wird unter der URL angezeigt, die in der Ausgabe der Push-Operation aufgelistet ist. Sie können auch den folgenden Befehl absetzen, um den Status der App zu prüfen und ihre URL anzuzeigen.

  ```
ibmcloud cf apps
  ```
  {: codeblock}

## Schritt 5: Fügen Sie eine Datenbank hinzu.
{: #add_database}

Als Nächstes werden Sie dieser Anwendung eine {{site.data.keyword.cloudant_short_notm}} NoSQL-Datenbank hinzufügen und die Anwendung so einrichten, dass sie lokal und unter {{site.data.keyword.Bluemix_notm}} ausgeführt werden kann.

1. Melden Sie sich in Ihrem Browser bei {{site.data.keyword.Bluemix_notm}} an und wechseln Sie zum Dashboard. Wählen Sie **Ressource erstellen** aus.
2. Wählen Sie den Abschnitt **Daten und Analyse** und anschließend **{{site.data.keyword.cloudant_short_notm}}** aus und erstellen Sie Ihren Service.
3. Rufen Sie die Ansicht **Verbindungen** auf. Wählen Sie Ihre Anwendung und anschließend **Verbindung erstellen** aus.
4. Wählen Sie **Erneutes Staging** aus, wenn Sie dazu aufgefordert werden. {{site.data.keyword.Bluemix_notm}} startet Ihre Anwendung erneut und stellt die Datenbankberechtigungsnachweise für Ihre Anwendung durch die Umgebungsvariable `VCAP_SERVICES` bereit. Diese Umgebungsvariable ist nur dann für die Anwendung verfügbar, wenn sie unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Umgebungsvariablen ermöglichen es Ihnen, die Bereitstellungseinstellungen von Ihrem Quellcode zu trennen. Anstelle der festen Codierung eines Datenbankkennworts können Sie dieses in einer Umgebungsvariablen speichern, auf die Sie in Ihrem Quellcode verweisen.
{: tip}

## Schritt 6: Verwenden Sie die Datenbank.
{: #use_database}
Sie werden jetzt Ihren lokalen Code aktualisieren, um auf diese Datenbank zu verweisen. Sie erstellen nun eine Datei '.env', in der die Berechtigungsnachweise für die Services gespeichert werden, die die Anwendung verwenden soll. Diese Datei wird NUR dann verwendet, wenn die Anwendung lokal ausgeführt wird. Bei der Ausführung in {{site.data.keyword.Bluemix_notm}} werden die Berechtigungsnachweise aus der Umgebungsvariablen VCAP_SERVICES gelesen.

1. Erstellen Sie eine Datei mit dem Namen `.env` im Verzeichnis `get-started-go` mit dem folgenden Inhalt:

  ```
CLOUDANT_URL=
  ```
  {: codeblock}

2. Wechseln Sie in Ihrem Browser zum {{site.data.keyword.Bluemix_notm}}-Dashboard und wählen Sie **_Ihre App_ > Verbindungen** aus. Klicken Sie auf das {{site.data.keyword.cloudant_short_notm}}-Menüsymbol (**&vellip;**) und wählen Sie **Berechtigungsnachweise anzeigen** aus.

3. Kopieren Sie einfach die `url` aus den Berechtigungsnachweisen in das Feld `CLOUDANT_URL` der Datei `.env` und speichern Sie die Änderungen.  Als Ergebnis erhalten Sie in etwa Folgendes:

  ```
CLOUDANT_URL=https://123456789 ... bluemix.cloudant.com
  ```
  {: codeblock}

4. Führen Sie Ihre Anwendung lokal aus.

  ```
go run main.go
  ```
  {: codeblock}

  Zeigen Sie Ihre App unter der folgenden URL an: http://localhost:8080. Alle Namen, die Sie in die App eingegeben haben, werden der Datenbank jetzt hinzugefügt.

Ihre lokale App und die {{site.data.keyword.Bluemix_notm}}-App verwenden die Datenbank gemeinsam.  Ihre {{site.data.keyword.Bluemix_notm}}-App wird unter der URL angezeigt, die in der Ausgabe der oben erwähnten Push-Operation aufgelistet wird.  Namen, die Sie in einer der Apps eingeben, sollten nach einer Aktualisierung des Browsers in beiden angezeigt werden.


Wenn Sie Ihre App nicht benötigen, stoppen Sie sie, damit keine unerwarteten Gebühren anfallen.
{: tip}

## Nächste Schritte

* [Lernprogramme](/docs/tutorials/index.html)
* [Beispiele ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
