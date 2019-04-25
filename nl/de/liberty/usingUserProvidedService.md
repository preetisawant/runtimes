---

copyright:
  years: 2017, 2018
lastupdated: "2018-6-26"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Vom Benutzer bereitgestellten Service mit Liberty in {{site.data.keyword.cloud_notm}} verwenden
{: #using_user_provided}

Cloud Foundry stellt ein Verfahren bereit, mit dem Services verbunden und verwendet werden können, die nicht zwingend von der
{{site.data.keyword.Bluemix_notm}}-Umgebung bereitgestellt werden oder in dieser verfügbar sind.
Bei dieser Funktion handelt es sich um [vom Benutzer bereitgestellte Services](https://docs.cloudfoundry.org/devguide/services/user-provided.html).

In diesem Dokument wird von den folgenden Voraussetzungen ausgegangen:
  * Es ist ein Service verfügbar.
  * Sie können Berechtigungsnachweise für diesen Service abrufen.
In diesem Dokument werden die Schritte beschrieben, die erforderlich sind, um eine Verbindung für diesen Service herzustellen
und ihn mit der Beispielanwendung zur Einführung in Liberty zu verwenden.

Für diese Beschreibung wird die CloudantNoSQLDB-Instanz als Beispielservice verwendet und
ein vom Benutzer bereitgestellter Service erstellt, für den eine Verbindung dazu hergestellt wird.

## Schritt 1: Einführungsanwendung mit einer Push-Operation bereitstellen
{: #follow_getting_started}

Führen Sie die Schritte im [Lernprogramm zur Einführung](/docs/runtimes/liberty/getting-started.html) bis zur Bereitstellung
der Anwendung per Push-Operation in {{site.data.keyword.Bluemix_notm}} aus.  Stoppen Sie von dem Herstellen einer Verbindung zur Datenbank.

## Schritt 2: CloudantNoSQLDB-Instanz erstellen
{: #create_cloudantnosqldb}

Führen Sie die Schritte im [Lernprogramm zur Einführung](/docs/runtimes/liberty/getting-started.html) aus,
um eine CloudantNoSqLDB-Instanz zu erstellen.

Verwenden Sie die Option zum Anzeigen der Berechtigungsnachweise, um die Berechtigungsnachweise von CloudandNoSQLDB zu kopieren. Speichern Sie diese Berechtigungsnachweise in einer lokalen Datei, z. B. 'cloudant-creds'.

## Schritt 3: Einen vom Benutzer bereitgestellten Service erstellen
Zur Verwendung der Einführungsanwendung muss der Name des
vom Benutzer bereitgestellten Service die Zeichenfolge
"cloudantNoSQLDB" enthalten.  Die Einführungsanwendung führt ein
Parsing der VCAP-Servicevariablen durch und sucht nach einem vom
Benutzer bereitgestellten Service mit einem Namen, der "cloudantNoSQLDB" enthält.

        ibmcloud cf cups my-cloudantNoSQLDB-ups -p cloudant-creds

## Schritt 4: Eine Bindung für den vom Benutzer bereitgestellten Service erstellen und ein erneutes Staging für die App durchführen
Erstellen Sie eine Bindung für den vom Benutzer bereitgestellten Service an die Einführungsanwendung.

        ibmcloud cf bs GettingStartedLiberty my-cloudantNoSQLDB-ups

        ibmcloud cf restage GettingStartedLiberty

## Schritt 5: Bestätigen
Navigieren Sie zu Ihrer Anwendung und stellen Sie sicher,
dass Sie mehrere Namen zum Namensfeld hinzufügen können.
