---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Tomcat-Anwendungen mithilfe von IBM Eclipse Tools für {{site.data.keyword.Bluemix_notm}} entwickeln

Als alternative Möglichkeit zum Entwickeln und Bereitstellen von Anwendungen in {{site.data.keyword.Bluemix}} können Sie auch {{site.data.keyword.eclipsetoolsfull}} verwenden. IBM Eclipse Tools bietet Plug-ins, die in einer vorhandenen Eclipse-Umgebung installiert werden können, um die Integration Ihrer IDE (Integrated Development Environment) in {{site.data.keyword.Bluemix_notm}} zu unterstützen.

Bei dieser Prozedur werden dieselben allgemeinen Schritte wie im [Lernprogramme zur Einführung](getting-started.html) für Liberty verwendet. Bei der Verwendung von Eclipse richten Sie eine Entwicklungsumgebung ein, stellen eine App lokal und in der Cloud bereit und integrieren einen Datenbankservice in Ihrer App.

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
* [Apache Tomcat Version 8.0.41 ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}

## Schritt 1: Klonen Sie die Beispielapp.
{: #clone}

Klonen Sie zuerst die Beispielapp 'GitHub repo'.
  ```bash
git clone https://github.com/IBM-Bluemix/get-started-tomcat
  ```
  {: pre}

## Schritt 2: Erstellen Sie den Quellcode für Ihre Anwendung
{: #build_app}

Verwenden Sie Maven, um Ihren Quellcode zu erstellen und führen Sie die daraus resultierende App aus.

1. Wechseln Sie mithilfe der Befehlszeile in das Verzeichnis, in dem sich die Beispielapp befindet.

  ```
cd get-started-tomcat
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
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/GetStartedTomcat.war
    buildpack: java_buildpack
```
{: codeblock}

In dieser Datei 'manifest.yml' generiert **random-route: true** eine zufällige Route für Ihre App, um zu verhindern, dass Ihre Route mit anderen Routen kollidiert.  Wenn Sie möchten, können Sie **random-route: true** durch **host: myChosenHostName** ersetzen und einen Hostnamen Ihrer Wahl angeben. [Weitere Informationen...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## Schritt 4: Stellen Sie die App unter {{site.data.keyword.Bluemix_notm}} bereit.
{: #deploy}

Stellen Sie Ihre App in einer der folgenden Bluemix-Regionen bereit. Für die optimale Latenzzeit wählen Sie eine Region, die Ihren Benutzern am nächsten liegt.

|Region          |API-Endpunkt                             |
|:---------------|:-------------------------------|
| USA (Süden)       |https://api.ng.bluemix.net     |
| Großbritannien | https://api.eu-gb.bluemix.net  |
| Sydney         | https://api.au-syd.bluemix.net |
| Frankfurt     | https://api.eu-de.bluemix.net |

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

1. Stellen Sie sicher, dass Sie über [IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix) verfügen.

2. Importieren Sie das Beispiel `get-started-java` in Eclipse, indem Sie zu **Datei > Importieren > Maven > Vorhandene Maven-Projekte** wechseln.

3. Erstellen Sie eine Tomcat-Serverdefinition:
  - Klicken Sie in der Ansicht `Server` mit der rechten Maustaste auf -> `Neu` -> `Server`.
  - Wählen Sie `Apache` -> `Tomcat v8.0 Server` aus.
  - Wählen Sie Ihr Verzeichnis `tomcat-install-dir` aus.
  - Setzen Sie den Assistenten mit Standardoptionen fort, um zum Abschluss zu gelangen.

4. Führen Sie Ihre Anwendung lokal auf dem Apache-Server aus:
  - Klicken Sie mit der rechten Maustaste auf das Beispiel `GetStartedTomcat` und wählen Sie die Optionen `Ausführen als` -> `Auf Server ausführen` aus.
  - Suchen Sie den Tomcat-Server als lokalen Host, wählen Sie ihn aus und klicken Sie auf die Option zum Fertigstellen.
  - In wenigen Sekunden wird Ihre Anwendung unter folgender Adresse ausgeführt: http://localhost:8080/GetStartedTomcat/.

5. Führen Sie Ihre Anwendung unter {{site.data.keyword.Bluemix_notm}} aus:
  - Klicken Sie mit der rechten Maustaste auf das Beispiel `GetStartedTomcat` und wählen Sie die Optionen `Ausführen als` -> `Auf Server ausführen` aus.
  - Suchen Sie `{{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}}` und wählen Sie diesen Eintrag aus. Klicken Sie anschließend auf die Option zum Fertigstellen.
  - Ein Assistent wird Sie durch die Bereitstellungsoptionen führen. Stellen Sie sicher, dass Sie unter `Name` einen eindeutigen Namen für Ihre Anwendung angeben.
  - In wenigen Minuten sollte Ihre Anwendung unter der von Ihnen ausgewählten URL ausgeführt werden.

Jetzt haben Sie Ihren Code sowohl lokal als auch in der Cloud ausgeführt!

## Schritt 6: Fügen Sie eine Datenbank hinzu.
{: #add_database}

Als Nächstes werden wir eine {{site.data.keyword.cloudantfull}}-Datenbank zu dieser Anwendung hinzufügen und die Anwendung so einrichten, dass sie lokal und unter {{site.data.keyword.Bluemix_notm}} ausgeführt werden kann.

1. Melden Sie sich in Ihrem Browser bei {{site.data.keyword.Bluemix_notm}} an und wechseln Sie in das Dashboard. Wählen Sie **Ressource erstellen** aus.
2. Wählen Sie den Abschnitt **Data and Analytics** und anschließend **Cloudant NoSQL DB** aus und erstellen Sie Ihren Service.
3. Rufen Sie die Ansicht **Verbindungen** auf. Wählen Sie Ihre Anwendung und anschließend **Verbindung erstellen** aus.
4. Wählen Sie **Erneutes Staging** aus, wenn Sie dazu aufgefordert werden. {{site.data.keyword.Bluemix_notm}} startet Ihre Anwendung erneut und bietet die Datenbankberechtigungsnachweise für Ihre Anwendung unter Verwendung der Umgebungsvariablen `VCAP_SERVICES`. Diese Umgebungsvariable ist nur dann für die Anwendung verfügbar, wenn Sie unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Umgebungsvariablen ermöglichen es Ihnen, die Bereitstellungseinstellungen von Ihrem Quellcode zu trennen. Anstelle der festen Codierung eines Datenbankkennworts können Sie dieses in einer Umgebungsvariablen speichern, auf die Sie in Ihrem Quellcode verweisen. [Weitere Informationen...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Schritt 7: Verwenden Sie die Datenbank.
{: #use_database}
Wir werden jetzt Ihren lokalen Code aktualisieren, um auf diese Datenbank zu verweisen. Wir werden die Berechtigungsnachweise für die Services in einer Eigenschaftendatei speichern. Diese Datei wird NUR dann verwendet, wenn die Anwendung lokal ausgeführt wird. Bei der Ausführung in {{site.data.keyword.Bluemix_notm}} werden die Berechtigungsnachweise aus der Umgebungsvariablen VCAP_SERVICES gelesen.

1. Öffnen Sie zuerst Eclipse und dann die Datei 'src/main/resources/cloudant.properties':
  ```
  cloudant_url=
  ```
  {: pre}

2. Öffnen Sie in Ihrem Browser die Benutzerschnittstelle von {{site.data.keyword.Bluemix_notm}}, wählen Sie Ihre App -> Verbindungen -> Cloudant -> Berechtigungsnachweise anzeigen aus.

3. Kopieren Sie einfach die `url` aus den Berechtigungsnachweisen in das Feld `url` der Datei `cloudant.properties` und speichern Sie die Änderungen.  Als Ergebnis erhalten Sie in etwa Folgendes:
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```

4. Starten Sie den Tomcat-Server in Eclipse erneut aus der Ansicht `Server`.

  Aktualisieren Sie Ihre Browseransicht unter: http://localhost:8080/GetStartedTomcat/. Alle Namen, die Sie in die App eingegeben haben, werden jetzt zur Datenbank hinzugefügt.

  Ihre lokale App und die {{site.data.keyword.Bluemix_notm}}-App verwenden die Datenbank gemeinsam.  Ihre {{site.data.keyword.Bluemix_notm}}-App wird an der URL angezeigt, die in der Ausgabe der oben erwähnten Push-Operation aufgelistet ist.  Namen, die Sie in einer der Apps eingeben, sollten nach einer Aktualisierung des Browsers in beiden angezeigt werden.

Denken Sie daran, dass Sie Ihre App unter {{site.data.keyword.Bluemix_notm}} stoppen, wenn Sie nicht benötigt wird, damit Ihnen nicht unerwartete Gebühren belastet werden.
{: tip}  
