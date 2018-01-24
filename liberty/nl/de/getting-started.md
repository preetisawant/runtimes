---

copyright:
  years: 2017
lastupdated: "2017-12-15"

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

* {: download} Herzlichen Glückwunsch! Sie haben die Hello World-Beispielanwendung unter {{site.data.keyword.Bluemix}} bereitgestellt!  Befolgen Sie diesen schrittweisen Leitfaden, um zu starten. Oder laden Sie den <a class="xref" href="http://bluemix.net" target="_blank" title="(Beispielcode herunterladen)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Beispielcode herunterladen" />Beispielcode herunter</a> und beginnen Sie auf eigene Faust.

Wenn Sie dem Lernprogramm zur Einführung für Liberty for Java folgen, werden Sie eine Entwicklungsumgebung einrichten, eine App lokal und unter {{site.data.keyword.Bluemix}} bereitstellen und einen Datenbankservice in Ihre App integrieren.

## Vorbemerkungen
{: #prereqs}

Sie benötigen die folgenden Konten und Tools:
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


## Schritt 2: Führen Sie die App lokal über die Befehlszeile aus.
{: #run_locally}

Verwenden Sie Maven, um Ihren Quellcode zu erstellen und führen Sie die daraus resultierende App aus.

1. Wechseln Sie mithilfe der Befehlszeile das Verzeichnis, in dem sich die Beispielapp befindet.

  ```
cd get-started-java
  ```
  {: pre}

1. Verwenden Sie Maven, um Abhängigkeiten zu installieren und die .war-Datei zu erstellen.

  ```
mvn clean install
  ```
  {: pre}

1. Führen Sie die App lokal unter Liberty aus.
  ```
mvn install liberty:run-server
  ```
  {: pre}

Wenn die Nachricht *The server defaultServer is ready to run a smarter planet.* angezeigt wird, finden Sie Ihre App unter folgender Adresse: http://localhost:9080/GetStartedJava.

Um Ihre App zu stoppen, drücken Sie *Strg-C* in dem Befehlszeilenfenster, in dem Sie die App gestartet haben.

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

| **Name der Region** | **Standort** | **API-Endpunkt** |
|-----------------|-------------------------|-------------------|
| Region USA (Süden) | Dallas, USA | api.ng.bluemix.net |
| Region USA (Osten) | Washington, DC, USA | api.us-east.bluemix.net |
| Region Großbritannien | London, England | api.eu-gb.bluemix.net |
| Region Sydney | Sydney, Australien | api.au-syd.bluemix.net |
| Region Deutschland | Frankfurt, Deutschland | api.eu-de.bluemix.net |
{: caption="Tabelle 1. {{site.data.keyword.cloud_notm}}-Regionsliste" caption-side="top"}

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


1. Übertragen Sie Ihre App mit einer Push-Operation aus dem Verzeichnis `get-started-java` zu {{site.data.keyword.Bluemix_notm}}.
  ```
cf push
  ```
  {: pre}

Das Bereitstellen Ihrer Anwendung kann einige Minuten dauern. Wenn die Bereitstellung abgeschlossen ist, sehen Sie eine Nachricht darüber, dass Ihre App ausgeführt wird. Ihre App wird an der URL angezeigt, die in der Ausgabe des Push-Befehls aufgelistet ist. Sie können aber auch den App-Bereitstellungsstatus und die URL anzeigen, indem Sie folgenden Befehl ausführen:
  ```
cf apps
  ```
  {: pre}

Sie können nach Fehlern im Bereitstellungsprozess suchen, indem Sie den Befehl `cf logs <Your-App-Name> --recent` verwenden.
{: tip}  

## Schritt 5: Fügen Sie eine Datenbank hinzu.
{: #add_database}

Als Nächstes werden wir eine NoSQL-Datenbank zu dieser Anwendung hinzufügen und die Anwendung so einrichten, dass sie lokal und unter {{site.data.keyword.Bluemix_notm}} ausgeführt werden kann.

1. Melden Sie sich in Ihrem Browser bei {{site.data.keyword.Bluemix_notm}} an und wechseln Sie in das Dashboard. Wählen Sie Ihre Anwendung durch Klicken auf den zugehörigen Namen in der Spalte **Name** aus.
2. Klicken Sie auf **Verbindungen** und dann auf **Verbindung erstellen**.
3. Wählen Sie im Abschnitt **Data & Analytics** den Eintrag **Cloudant NoSQL DB** aus und erstellen Sie dann den Service.
4. Wechseln Sie zu **Apps > Ihre App > Verbindungen** und wählen Sie anschließend **Vorhandenen verbinden** aus.
5. Wählen Sie **Erneutes Staging** aus, wenn Sie dazu aufgefordert werden. {{site.data.keyword.Bluemix_notm}} startet Ihre Anwendung erneut und bietet die Datenbankberechtigungsnachweise für Ihre Anwendung unter Verwendung der Umgebungsvariablen `VCAP_SERVICES`. Diese Umgebungsvariable ist nur dann für die Anwendung verfügbar, wenn Sie unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Umgebungsvariablen ermöglichen es Ihnen, die Bereitstellungseinstellungen von Ihrem Quellcode zu trennen. Anstelle der festen Codierung eines Datenbankkennworts können Sie dieses in einer Umgebungsvariablen speichern, auf die Sie in Ihrem Quellcode verweisen. [Weitere Informationen...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Schritt 7: Verwenden Sie die Datenbank.
{: #use_database}
Wir werden jetzt Ihren lokalen Code aktualisieren, um auf diese Datenbank zu verweisen. Wir werden die Berechtigungsnachweise für die Services in einer Eigenschaftendatei speichern. Diese Datei wird NUR dann verwendet, wenn die Anwendung lokal ausgeführt wird. Bei der Ausführung in {{site.data.keyword.Bluemix_notm}} werden die Berechtigungsnachweise aus der Umgebungsvariablen `VCAP_SERVICES` gelesen.

1. Wechseln Sie in Ihrem Browser zu {{site.data.keyword.Bluemix_notm}} und wählen Sie **Apps > _Ihre App_ > Verbindungen > Cloudant > Berechtigungsnachweise anzeigen** aus.

2. Kopieren Sie einfach die `url` aus dem Feld `url` der Datei `cloudant.properties` und speichern Sie die Änderungen.
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:pre}

3. Starten Sie den Server erneut.

  Aktualisieren Sie Ihre Browseransicht unter: http://localhost:9080/GetStartedJava/. Alle Namen, die Sie in die App eingegeben haben, werden jetzt zur Datenbank hinzugefügt.

  Ihre lokale App und die {{site.data.keyword.Bluemix_notm}}-App verwenden die Datenbank gemeinsam. Namen, die Sie in einer der Apps eingeben, werden nach einer Aktualisierung des Browsers in beiden angezeigt.

Denken Sie daran, dass Sie Ihre App unter {{site.data.keyword.Bluemix_notm}} stoppen, wenn Sie nicht benötigt wird, damit Ihnen nicht unerwartete Gebühren belastet werden.
{: tip}  

## Nächste Schritte

* [Lernprogramme](/docs/tutorials/index.html)
* [Beispiele ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
