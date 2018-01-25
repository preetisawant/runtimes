---

copyright:
  years: 2017
lastupdated: "2017-11-09"

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
* [IBM Eclipse Tools for IBM Cloud ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}
* [Eclipse IDE for Java EE Developers ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}

Wenn Sie das [Lernprogramm zur Einführung](getting-started.md) ausgeführt haben, haben Sie diese Tools und Konten möglicherweise bereits installiert. Stellen Sie vor dem Starten sicher, dass auch Folgendes installiert und registriert ist:
* [{{site.data.keyword.Bluemix_notm}}-Konto](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry-CLI ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://git-scm.com/downloads){: new_window}
* [Maven ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://maven.apache.org/download.cgi){: new_window}

## Schritt 1: Klonen Sie die Beispielapp.
{: #clone}

Klonen Sie zuerst die Beispielapp 'GitHub repo'.
  ```bash
git clone https://github.com/IBM-Bluemix/get-started-java
  ```
  {: pre}

## Schritt 2: Erstellen Sie den Quellcode für Ihre Anwendung
{: #build_app}

Verwenden Sie Maven, um Ihren Quellcode zu erstellen und führen Sie die daraus resultierende App aus.

1. Wechseln Sie mithilfe der Befehlszeile in das Verzeichnis, in dem sich die Beispielapp befindet.

  ```
cd get-started-java
  ```
  {: pre}

1. Verwenden Sie Maven, um Abhängigkeiten zu installieren und die .war-Datei zu erstellen.

  ```
mvn clean install
  ```
  {: pre}

## Schritt 3: Bereiten Sie die App für die Bereitstellung vor.
{: #prepare}

Für die Bereitstellung unter {{site.data.keyword.Bluemix_notm}} kann es hilfreich sein, die Datei 'manifest.yml' zu installieren. Die Datei 'manifest.yml' enthält Basisinformationen zu Ihrer App wie den Namen, wieviel Speicher für jede Instanz zugeordnet werden soll und die Route. Wir haben eine Beispieldatei 'manifest.yml' im Verzeichnis `get-started-java` bereitgestellt.

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

In dieser Datei 'manifest.yml' generiert **random-route: true** eine zufällige Route für Ihre App, um zu verhindern, dass Ihre Route mit anderen Routen kollidiert.  Wenn Sie möchten, können Sie **random-route: true** durch **host: myChosenHostName** ersetzen und einen Hostnamen Ihrer Wahl angeben. [Weitere Informationen...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## Schritt 4: Stellen Sie die App unter {{site.data.keyword.Bluemix_notm}} bereit.
{: #deploy}

Stellen Sie Ihre App in einer der folgenden {{site.data.keyword.Bluemix_notm}}-Regionen bereit. Für die optimale Latenzzeit wählen Sie eine Region, die Ihren Benutzern am nächsten liegt.

|Region          |API-Endpunkt                             |
|:---------------|:-------------------------------|
| USA (Süden)    | https://api.ng.bluemix.net     |
| Großbritannien | https://api.eu-gb.bluemix.net  |
| Sydney         | https://api.au-syd.bluemix.net |
| Frankfurt      | https://api.eu-de.bluemix.net |

1. Legen Sie den API-Endpunkt fest, indem Sie `<API-endpoint>` durch den Endpunkt Ihrer Region ersetzen.
  ```
cf api <API-endpoint>
  ```
  {: pre}

1. Melden Sie sich an Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an.
  ```
cf login
  ```
  {: pre}

  Wenn Sie sich nicht über den Befehl `cf login` oder `bx login` anmelden können, weil Sie über eine eingebundene Benutzer-ID verfügen, verwenden Sie entweder den Befehl `cf login --sso` oder den Befehl `bx login --sso`, um sich mit Ihrer Single-Sign-on-ID anzumelden. Weitere Informationen finden Sie unter [Mit eingebundener ID anmelden](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id).

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

  In wenigen Sekunden wird Ihre Anwendung unter folgender Adresse ausgeführt: http://localhost:9080/GetStartedJava.

5. Code aktualisieren:
  - Öffnen Sie die Datei `src/main/webapp/index.html` und ändern Sie die Kopfzeile von `<h1>Welcome.</h1>` in `<h1>Welcome Jane.</h1>`.
  - Speichern Sie Ihre Änderungen. Liberty wird Ihre Änderungen automatisch übernehmen.
  - Aktualisieren Sie Ihren Browser (http://localhost:9080/GetStartedJava), um die Änderungen anzuzeigen.

6. Übergeben Sie Ihre Änderungen mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}}:
  - Erstellen Sie in der Befehlszeile aus dem Verzeichnis `get-started-java` die .war-Datei erneut:
    ```
mvn clean install
    ```
    {: pre}
  - Übergeben Sie Ihre Anwendung mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}}.
    ```
cf push
    ```
    {: pre}

Jetzt haben Sie Ihren Code sowohl lokal als auch in der Cloud ausgeführt!

## Schritt 6: Fügen Sie eine Datenbank hinzu.
{: #add_database}

Als Nächstes werden wir eine NoSQL-Datenbank zu dieser Anwendung hinzufügen und die Anwendung so einrichten, dass sie lokal und unter {{site.data.keyword.Bluemix_notm}} ausgeführt werden kann.

1. Melden Sie sich in Ihrem Browser bei {{site.data.keyword.Bluemix_notm}} an und wechseln Sie in das Dashboard. Wählen Sie Ihre Anwendung durch Klicken auf den zugehörigen Namen in der Spalte **Name** aus.
2. Klicken Sie auf **Verbindungen** und dann auf **Neuen verbinden**.
3. Wählen Sie im Abschnitt **Data & Analytics** den Eintrag **Cloudant NoSQL DB** aus und erstellen Sie dann den Service.
4. Wechseln Sie zu **Apps > Ihre App > Verbindungen** und wählen Sie anschließend **Vorhandenen verbinden** aus.
5. Wählen Sie **Erneutes Staging** aus, wenn Sie dazu aufgefordert werden. {{site.data.keyword.Bluemix_notm}} startet Ihre Anwendung erneut und bietet die Datenbankberechtigungsnachweise für Ihre Anwendung unter Verwendung der Umgebungsvariablen `VCAP_SERVICES`. Diese Umgebungsvariable ist nur dann für die Anwendung verfügbar, wenn Sie unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Umgebungsvariablen ermöglichen es Ihnen, die Bereitstellungseinstellungen von Ihrem Quellcode zu trennen. Anstelle der festen Codierung eines Datenbankkennworts können Sie dieses in einer Umgebungsvariablen speichern, auf die Sie in Ihrem Quellcode verweisen. [Weitere Informationen...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Schritt 7: Verwenden Sie die Datenbank.
{: #use_database}
Wir werden jetzt Ihren lokalen Code aktualisieren, um auf diese Datenbank zu verweisen. Wir werden die Berechtigungsnachweise für die Services in einer Eigenschaftendatei speichern. Diese Datei wird NUR dann verwendet, wenn die Anwendung lokal ausgeführt wird. Bei der Ausführung in {{site.data.keyword.Bluemix_notm}} werden die Berechtigungsnachweise aus der Umgebungsvariablen `VCAP_SERVICES` gelesen.

1. Öffnen Sie in Eclipse die Datei 'src/main/resources/cloudant.properties':
  ```
  cloudant_url=
  ```
  {: pre}

2. Wechseln Sie in Ihrem Browser zu {{site.data.keyword.Bluemix_notm}} und wählen Sie **Apps > _Ihre App_ > Verbindungen > Cloudant > Berechtigungsnachweise anzeigen** aus.

3. Kopieren Sie einfach die `url` aus dem Feld `url` der Datei `cloudant.properties` und speichern Sie die Änderungen.
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:pre}

4. Starten Sie den Liberty-Server in Eclipse erneut aus der Ansicht `Server`.

  Aktualisieren Sie Ihre Browseransicht unter: http://localhost:9080/GetStartedJava/. Alle Namen, die Sie in die App eingegeben haben, werden jetzt zur Datenbank hinzugefügt.

  Ihre lokale App und die {{site.data.keyword.Bluemix_notm}}-App verwenden die Datenbank gemeinsam. Namen, die Sie in einer der Apps eingeben, werden nach einer Aktualisierung des Browsers in beiden angezeigt.


Denken Sie daran, dass Sie Ihre App unter {{site.data.keyword.Bluemix_notm}} stoppen, wenn Sie nicht benötigt wird, damit Ihnen nicht unerwartete Gebühren belastet werden.
{: tip}  
