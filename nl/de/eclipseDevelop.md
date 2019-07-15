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

# Anwendungen mithilfe von IBM Eclipse Tools für {{site.data.keyword.cloud_notm}} entwickeln

Als alternative Möglichkeit zum Entwickeln und Bereitstellen von Anwendungen in {{site.data.keyword.Bluemix}} können Sie auch {{site.data.keyword.eclipsetoolsfull}} verwenden. {{site.data.keyword.eclipsetoolsfull}} bietet Plug-ins, die in einer vorhandenen Eclipse-Umgebung installiert werden können, um die Integration Ihrer IDE (Integrated Development Environment) in {{site.data.keyword.Bluemix_notm}} zu unterstützen.

Bei dieser Prozedur werden dieselben allgemeinen Schritte wie im [Lernprogramme zur Einführung](getting-started.html) für Liberty verwendet. Bei der Verwendung von Eclipse richten Sie eine Entwicklungsumgebung ein, stellen eine App lokal und in der Cloud bereit und integrieren einen {{site.data.keyword.Bluemix_notm}}-Datenbankservice in Ihrer App.

## Vorbemerkungen
{: #prereqs}

Sie benötigen die folgenden Konten und Tools:
* [IBM Eclipse Tools for IBM Cloud ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}
* [Eclipse IDE for Java EE Developers ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}

Wenn Sie das [Lernprogramm zur Einführung](getting-started.md) ausgeführt haben, haben Sie diese Tools und Konten möglicherweise bereits installiert. Stellen Sie vor dem Starten sicher, dass auch Folgendes installiert und registriert ist:
* [{{site.data.keyword.Bluemix_notm}}-Konto](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}}-CLI](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://git-scm.com/downloads){: new_window}
* [Maven ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://maven.apache.org/download.cgi){: new_window}

## Schritt 1: Klonen Sie die Beispielapp.
{: #clone}

Klonen Sie zuerst die Beispielapp 'GitHub repo'.

  ```
git clone https://github.com/IBM-Cloud/get-started-java
  ```
  {: codeblock}

## Schritt 2: Erstellen Sie den Quellcode für Ihre Anwendung
{: #build_app}

Verwenden Sie Maven, um Ihren Quellcode zu erstellen, und führen Sie die daraus resultierende App aus.

1. Wechseln Sie in der Befehlszeile in das Verzeichnis, in dem sich die Beispielapp befindet.

  ```
cd get-started-java
  ```
  {: codeblock}

1. Verwenden Sie Maven, um Abhängigkeiten zu installieren und die .war-Datei zu erstellen.

  ```
mvn clean install
  ```
  {: codeblock}

## Schritt 3: Bereiten Sie die App für die Bereitstellung vor.
{: #prepare}

Für die Bereitstellung unter {{site.data.keyword.Bluemix_notm}} kann es hilfreich sein, die Datei 'manifest.yml' zu installieren. Die Datei 'manifest.yml' enthält Basisinformationen zu Ihrer App wie den Namen, die Speichergröße, die für jede Instanz zugeordnet werden soll, und die Route. Eine Beispieldatei 'manifest.yml' wird im Verzeichnis `get-started-java` bereitgestellt.

Öffnen Sie die Datei 'manifest.yml' und ändern Sie die Angabe für `name` von `GetStartedJava` in den Namen Ihrer App <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

In dieser Datei 'manifest.yml' generiert **random-route: true** eine zufällige Route für Ihre App, um zu verhindern, dass Ihre Route mit anderen Routen kollidiert.  Wenn Sie möchten, können Sie **random-route: true** durch **host: myChosenHostName** ersetzen und einen Hostnamen Ihrer Wahl angeben.
{: tip}

## Schritt 4: Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.
{: #deploy}

1. Melden Sie sich an Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an und wählen Sie einen API-Endpunkt aus.

  ```
ibmcloud login
  ```
  {: codeblock}

  Wenn Sie sich nicht mit `ibmcloud login` anmelden können, weil Sie eine eingebundene Benutzer-ID haben, verwenden Sie den folgenden Befehl, um sich mit Ihrer Single Sign-on-ID anzumelden. Weitere Informationen finden Sie unter [Mit eingebundener ID anmelden](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id).

  ```
ibmcloud login --sso
  ```
  {: codeblock}

  Legen Sie als Nächstes die Cloud Foundry-CLI als Ziel fest:

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Wenn Sie keine eingerichtete Organisation oder keinen eingerichteten Bereich haben, finden Sie weitere Informationen unter [Organisationen und Bereiche hinzufügen](https://console.bluemix.net/docs/account/orgs_spaces.html).
  {: tip}

## Schritt 5: Entwickeln Sie mit Eclipse.
{: #eclipse}

1. Stellen Sie sicher, dass Sie über [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix) verfügen.

2. Importieren Sie das Beispiel `get-started-java` in Eclipse, indem Sie zu **Datei > Importieren > Maven > Vorhandene Maven-Projekte** wechseln.

3. Erstellen Sie eine Liberty-Serverdefinition. Die folgenden Schritte werden einen neuen Liberty-Server herunterladen.
  - Klicken Sie in der Ansicht **Fenster > Ansicht anzeigen > Server** mit der rechten Maustaste und wählen Sie **Neu > Server** aus.
  - Wählen Sie **IBM > WebSphere Application Server Liberty** aus.
  - Wählen Sie **Von einem Archiv oder einem Repository installieren** aus.
  - Wenn Sie dazu aufgefordert werden, geben Sie einen Zielpfad zu einem neuen Ordner ein (/Users/username/liberty), in dem Sie Liberty installieren möchten.
  - Wählen Sie **Neue Laufzeitumgebung von ibm.com herunterladen und installieren** aus.
  - Wählen Sie **Webprofil für WAS-Liberty mit Java EE 7** aus.
  - Setzen Sie den Assistenten mit Standardoptionen fort, um zum Abschluss zu gelangen.

4. Führen Sie Ihre Anwendung lokal unter Liberty aus:
  - Ändern Sie die Einstellungen für den Web-Browser in den Systemstandardwert, indem Sie **Fenster > Web-Browser > Standard-Web-Browser des Systems** auswählen.
  - Klicken Sie mit der rechten Maustaste auf das Beispiel `GetStartedJava` und wählen Sie **Ausführen als > Auf Server ausführen** aus.
  - Suchen Sie den Liberty-Server als lokalen Host, wählen Sie ihn aus und klicken Sie auf die Option zum **Fertigstellen**.

  Nach wenigen Sekunden wird Ihre Anwendung unter folgender Adresse ausgeführt: http://localhost:9080/GetStartedJava.

5. Code aktualisieren:
  - Öffnen Sie die Datei `src/main/webapp/index.html` und ändern Sie die Kopfzeile von `<h1>Welcome.</h1>` in `<h1>Welcome Jane.</h1>`.
  - Speichern Sie Ihre Änderungen. Liberty wird Ihre Änderungen automatisch übernehmen.
  - Aktualisieren Sie Ihren Browser (http://localhost:9080/GetStartedJava), um die Änderungen anzuzeigen.

6. Übertragen Sie Ihre Änderungen mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}}:
  - Erstellen Sie in der Befehlszeile aus dem Verzeichnis `get-started-java` die .war-Datei erneut:

    ```
mvn clean install
    ```
    {: codeblock}

  - Übergeben Sie Ihre Anwendung mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}}.

    ```
ibmcloud cf push
    ```
    {: codeblock}

Jetzt haben Sie Ihren Code sowohl lokal als auch in der Cloud ausgeführt!

## Schritt 6: Fügen Sie eine Datenbank hinzu.
{: #add_database}

Als Nächstes werden Sie dieser Anwendung eine NoSQL-Datenbank hinzufügen und die Anwendung so einrichten, dass sie lokal und unter {{site.data.keyword.Bluemix_notm}} ausgeführt werden kann.

1. Melden Sie sich in Ihrem Browser bei {{site.data.keyword.Bluemix_notm}} an und wechseln Sie zum Dashboard. Wählen Sie **Ressource erstellen** aus.
2. Wählen Sie den Abschnitt **Daten und Analyse** und anschließend **{{site.data.keyword.cloudant_short_notm}}** aus und erstellen Sie Ihren Service.
3. Rufen Sie die Ansicht **Verbindungen** auf. Wählen Sie Ihre Anwendung und anschließend **Verbindung erstellen** aus.
4. Wählen Sie **Erneutes Staging** aus, wenn Sie dazu aufgefordert werden. {{site.data.keyword.Bluemix_notm}} startet Ihre Anwendung erneut und stellt die Datenbankberechtigungsnachweise für Ihre Anwendung durch die Umgebungsvariable `VCAP_SERVICES` bereit. Diese Umgebungsvariable ist nur dann für die Anwendung verfügbar, wenn sie unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Umgebungsvariablen ermöglichen es Ihnen, die Bereitstellungseinstellungen von Ihrem Quellcode zu trennen. Anstelle der festen Codierung eines Datenbankkennworts können Sie dieses in einer Umgebungsvariablen speichern, auf die Sie in Ihrem Quellcode verweisen.
{: tip}

## Schritt 7: Verwenden Sie die Datenbank.
{: #use_database}
Sie werden jetzt Ihren lokalen Code aktualisieren, um auf diese Datenbank zu verweisen. Sie werden die Berechtigungsnachweise für die Services in einer Eigenschaftendatei speichern. Diese Datei wird NUR dann verwendet, wenn die Anwendung lokal ausgeführt wird. Bei der Ausführung in {{site.data.keyword.Bluemix_notm}} werden die Berechtigungsnachweise aus der Umgebungsvariablen `VCAP_SERVICES` gelesen.

1. Öffnen Sie in Eclipse die Datei 'src/main/resources/cloudant.properties':

  ```
  cloudant_url=
  ```
  {: codeblock}

2. Wechseln Sie in Ihrem Browser zu {{site.data.keyword.Bluemix_notm}} und wählen Sie **Apps > _Ihre App_ > Verbindungen > Cloudant > Berechtigungsnachweise anzeigen** aus.

3. Kopieren Sie einfach die `url` aus den Berechtigungsnachweisen in das Feld `url` der Datei `cloudant.properties` und speichern Sie die Änderungen.

  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:codeblock}

4. Starten Sie den Liberty-Server in Eclipse erneut aus der Ansicht `Server`.

  Aktualisieren Sie Ihre Browseransicht unter: http://localhost:9080/GetStartedJava/. Alle Namen, die Sie in die App eingegeben haben, werden der Datenbank jetzt hinzugefügt.

  Ihre lokale App und die {{site.data.keyword.Bluemix_notm}}-App verwenden die Datenbank gemeinsam. Namen, die Sie in einer der Apps eingeben, werden nach einer Aktualisierung des Browsers in beiden angezeigt.


Denken Sie daran, dass Sie Ihre App unter {{site.data.keyword.Bluemix_notm}} stoppen, wenn Sie sie nicht benötigen, damit keine unerwarteten Gebühren anfallen.
{: tip}  
