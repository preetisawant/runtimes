---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-14"

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

* {: download} Herzlichen Glückwunsch! Sie haben die Hello World-Beispielanwendung unter {{site.data.keyword.Bluemix}} bereitgestellt!  Befolgen Sie diesen schrittweisen Leitfaden, um zu starten. Oder laden Sie den <a class="xref" href="http://bluemix.net" target="_blank" title="(Beispielcode herunterladen)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Anwendungscode herunterladen" />Beispielcode herunter</a> und beginnen Sie auf eigene Faust.

Wenn Sie diesem Lernprogramm folgen, werden Sie eine Entwicklungsumgebung einrichten, eine App lokal und unter {{site.data.keyword.Bluemix}} bereitstellen und einen {{site.data.keyword.Bluemix_notm}}-Datenbankservice in Ihre App integrieren.

## Vorbemerkungen
{: #prereqs}
* [Git ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://git-scm.com/downloads){: new_window}
* [Cloud Foundry-CLI ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Swift-Compiler ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://swift.org/download/) für Ihre Plattform.

## Schritt 1: Klonen Sie die Beispielapp.
{: #clone}

Jetzt können Sie beginnen, mit der einfachen Swift-App zu arbeiten. Klonen Sie das Repository und wechseln Sie in das Verzeichnis, in dem sich die Beispielapp befindet.
  ```
git clone https://github.com/IBM-Bluemix/get-started-swift
  ```
  {: pre}

  ```
cd get-started-swift
  ```
  {: pre}

  Lesen Sie die Dateien im Verzeichnis *get-started-swift*, um sich mit deren Inhalt vertraut zu machen.

## Schritt 2: Führen Sie die App lokal aus.
{: #run_locally}

Sobald Sie den Swift-Compiler installiert und dieses Git-Repository geklont haben, können Sie die Anwendung kompilieren und ausführen. Wechseln Sie in das Stammverzeichnis dieses Repositorys in Ihrem System und geben Sie den folgenden Befehl aus:
```
swift build
```
{: pre}

Die Ausführung dieses Befehls kann einige Minuten dauern.

Sobald die Anwendung erfolgreich kompiliert wurde, können Sie die ausführbare Datei, die vom Swift-Compiler generiert wurde, ausführen.
```
.build/debug/get-started-swift
```
{: pre}

Sie sollten eine Ausgabe ähnlich der folgenden sehen:

```
Server is listening on port: 8080
```
{: codeblock}

Ihre App finden Sie unter http://localhost:8080.

## Schritt 3: Bereiten Sie die App für die Bereitstellung vor.
{: #prepare}

Für die Bereitstellung unter {{site.data.keyword.Bluemix_notm}} kann es hilfreich sein, die Datei 'manifest.yml' zu installieren. Die Datei 'manifest.yml' enthält Basisinformationen zu Ihrer App wie den Namen, wieviel Speicher für jede Instanz zugeordnet werden soll und die Route. Wir haben eine Beispieldatei 'manifest.yml' im Verzeichnis `get-started-swift` bereitgestellt.

Öffnen Sie die Datei 'manifest.yml' und ändern Sie die Angabe für `name` von `GetStartedSwift` in den Namen Ihrer App <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedSwift
     random-route: true
     memory: 256M
     command: kitura-helloworld
     buildpack: swift_buildpack
  ```
  {: codeblock}

In dieser Datei 'manifest.yml' generiert **random-route: true** eine zufällige Route für Ihre App, um zu verhindern, dass Ihre Route mit anderen Routen kollidiert.  Wenn Sie möchten, können Sie **random-route: true** durch **host: myChosenHostName** ersetzen und einen Hostnamen Ihrer Wahl angeben. [Weitere Informationen...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## Schritt 4: Stellen Sie die App bereit.
{: #deploy}

Sie können die Cloud Foundry-CLI verwenden, um Apps bereitzustellen.

Wählen Sie Ihren API-Endpunkt aus.
  ```
cf api <API-endpoint>
  ```
  {: pre}

Ersetzen Sie *API-endpoint* im Befehl durch einen API-Endpunkt aus der folgenden Liste:

| **Name der Region** | **Standort** | **API-Endpunkt** |
|-----------------|-------------------------|-------------------|
| Region USA (Süden) | Dallas, USA | api.ng.bluemix.net |
| Region USA (Osten) | Washington, DC, USA | api.us-east.bluemix.net |
| Region Großbritannien | London, England | api.eu-gb.bluemix.net |
| Region Sydney | Sydney, Australien | api.au-syd.bluemix.net |
| Region Deutschland | Frankfurt, Deutschland | api.eu-de.bluemix.net |
{: caption="Tabelle 1. {{site.data.keyword.cloud_notm}}-Regionsliste" caption-side="top"}

Melden Sie sich bei Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an.

   ```
 cf login
   ```
   {: pre}

Wenn Sie sich nicht über den Befehl `cf login` oder `bx login` anmelden können, weil Sie über eine eingebundene Benutzer-ID verfügen, verwenden Sie entweder den Befehl `cf login --sso` oder den Befehl `bx login --sso`, um sich mit Ihrer Single-Sign-on-ID anzumelden. Weitere Informationen finden Sie unter [Mit eingebundener ID anmelden](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id).

Übertragen Sie Ihre App aus dem Verzeichnis *get-started-swift* mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}}.
   ```
 cf push
   ```
   {: pre}

Dieser Vorgang kann einige Minuten dauern. Falls ein Fehler im Bereitstellungsprozess auftritt, können Sie mithilfe des Befehls `cf logs <Your-App-Name> --recent` nach dem Fehler suchen.

Wenn die Bereitstellung abgeschlossen ist, sollten Sie eine Nachricht sehen, die anzeigt, dass Ihre App ausgeführt wird.  Ihre App wird an der URL angezeigt, die in der Ausgabe der Push-Operation aufgelistet ist.  Sie können auch den Befehl `cf apps` ausgeben, um Ihren Appstatus und die URL anzuzeigen.

## Schritt 5: Fügen Sie eine Datenbank hinzu.
{: #add_database}

Als Nächstes werden wir eine NoSQL-Datenbank zu dieser Anwendung hinzufügen und die Anwendung so einrichten, dass sie lokal und unter {{site.data.keyword.Bluemix_notm}} ausgeführt werden kann.

1. Melden Sie sich in Ihrem Browser bei {{site.data.keyword.Bluemix_notm}} an und wechseln Sie in das Dashboard. Wählen Sie **Ressource erstellen** aus.
2. Wählen Sie den Abschnitt **Data and Analytics** und anschließend **Cloudant NoSQL DB** aus und erstellen Sie Ihren Service.
3. Rufen Sie die Ansicht **Verbindungen** auf. Wählen Sie Ihre Anwendung und anschließend **Verbindung erstellen** aus.
4. Wählen Sie **Erneutes Staging** aus, wenn Sie dazu aufgefordert werden. {{site.data.keyword.Bluemix_notm}} startet Ihre Anwendung erneut und bietet die Datenbankberechtigungsnachweise für Ihre Anwendung unter Verwendung der Umgebungsvariablen `VCAP_SERVICES`. Diese Umgebungsvariable ist nur dann für die Anwendung verfügbar, wenn Sie unter {{site.data.keyword.Bluemix_notm}} ausgeführt wird.

Umgebungsvariablen ermöglichen es Ihnen, die Bereitstellungseinstellungen von Ihrem Quellcode zu trennen. Anstelle der festen Codierung eines Datenbankkennworts können Sie dieses in einer Umgebungsvariablen speichern, auf die Sie in Ihrem Quellcode verweisen. [Weitere Informationen...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Schritt 6: Verwenden Sie die Datenbank.
{: #use_database}

Wir werden jetzt Ihren lokalen Code aktualisieren, um auf diese Datenbank zu verweisen. Erstellen Sie eine json-Datei, die die Berechtigungsnachweise für die Services speichert, die die Anwendung verwendet. Diese Datei wird NUR dann verwendet, wenn die Anwendung lokal ausgeführt wird. Bei der Ausführung in {{site.data.keyword.Bluemix_notm}} werden die Berechtigungsnachweise aus der Umgebungsvariablen VCAP_SERVICES gelesen.

Erstellen Sie eine Datei mit dem Namen `my-cloudant-credentials.json` im Verzeichnis `config` mit dem folgenden Inhalt (als Referenz siehe `config/my-cloudant-credentials.json.example`):

 ```
 {
   "password": "<password>",
   "url": "<url>",
   "username": "<username>"
 }
 ```

Aktualisieren Sie die Datei `mappings.json` im Verzeichnis `config`, indem Sie den Platzhalter `cloudant` durch den **Namen** Ihrer DB-Instanz ersetzen:

```
{
  "MyCloudantDB": {
    "searchPatterns": [
      "cloudfoundry:cloudant",
      "env:kube-cloudant-credentials",
      "file:config/my-cloudant-credentials.json"
    ]
  }
}
```

Diese Beispielanwendung verwendet das Paket `CloudEnvironment` für die Interaktion mit {{site.data.keyword.Bluemix_notm}}, um ein Parsing für Umgebungsvariablen durchzuführen. [Weitere Informationen...](https://packagecatalog.com/package/IBM-Swift/CloudEnvironment)

Der Platzhalter `cloudant` in der Konfiguration `cloudfoundry:cloudant` erleichtert das Binden eines vom Benutzer bereitgestellten Cloudant-Service an Ihre Anwendung. Mit der Konfiguration `cloudfoundry:cloudant` können Sie einen Cloudant-Service erstellen, der die Zeichenfolge `cloudant` im Servicenamen enthält und den Service an Ihre Anwendung bindet, ohne die Datei `config.json` zu bearbeiten. Wenn Sie diese Konfiguration ändern und zu einem späteren Zeitpunkt einen vom Benutzer bereitgestellten Cloudant-Service verwenden möchten, müssen Sie entweder die Konfiguration für `cloudfoundry:cloudant` bearbeiten oder `cloudfoundry:` mit dem Namen des vom Benutzer bereitgestellten Service definieren.
{: tip}

Kehren Sie in die Benutzerschnittstelle von {{site.data.keyword.Bluemix_notm}} zurück und wählen Sie Ihre App -> Verbindungen -> Cloudant -> Berechtigungsnachweise anzeigen aus.

Kopieren Sie einfach die Berechtigungsnachweise und fügen Sie diese in die entsprechendne Felder in Ihrer lokalen Datei 'config.json' ein.

Erstellen Sie einen Build und führen Sie Ihre Anwendung lokal aus.
 ```
swift build  
 ```
 {: pre}

  ```
.build/debug/kitura-helloworld
 ```
 {: pre}

Ihre App finden Sie unter: http://localhost:8080. Alle Namen, die Sie in die App eingegeben haben, werden jetzt zur Datenbank hinzugefügt.

 Diese Beispielanwendung verwendet das 'Kitura-CouchDB'-Paket für die Interaktion mit Cloudant. [Weitere Informationen...](https://packagecatalog.com/package/IBM-Swift/Kitura-CouchDB)

 Nehmen Sie alle gewünschten Änderungen vor und stellen Sie die App erneut in {{site.data.keyword.Bluemix_notm}} bereit!

 ```
 cf app push
 ```

 Ihre App wird an der URL angezeigt, die in der Ausgabe der Push-Operation aufgelistet ist, zum Beispiel *myUrl.mybluemix.net*.

Denken Sie daran, dass Sie Ihre App stoppen, wenn Sie nicht benötigt wird, damit Ihnen nicht unerwartete Gebühren belastet werden.
{: tip}

## Nächste Schritte

* [Lernprogramme](/docs/tutorials/index.html)
* [Beispiele ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
