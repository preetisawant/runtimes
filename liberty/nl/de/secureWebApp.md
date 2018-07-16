---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Sichere Java-Webanwendungen schreiben
{: #secure_java_web_app}

Alle Webanwendungen müssen unter Berücksichtigung von Sicherheitsaspekten gestaltet und codiert werden, um das Auftreten schwerwiegender Sicherheitslücken zu vermeiden.
{: shortdesc}

{{site.data.keyword.Bluemix}} bietet eine sichere Starteranwendung, damit Sie sichereren Liberty Java-Code schreiben können und die meisten der XSS-Probleme (XSS, Cross-Site Scripting) vermeiden. Sie können diese [sichere Starteranwendung](https://github.com/IBM-Cloud/java-secure-app) herunterladen, einen Build erstellen und das Ergebnis lokal und unter {{site.data.keyword.Bluemix_notm}} bereitstellen.

## Warum sollen sichere Web-Apps geschrieben werden?
{: #why}

Eine Sicherheitslücke kann durch unterschiedliche Attacken ausgenutzt werden. Eine Attacke kann Berechtigungsnachweise stehlen, zu Daten- und Funktionsverlust führen, Services unterbrechen und der Reputation und dem Umsatz des Unternehmens schaden. Cross-Site Scripting (XSS) ist eine der bekannten Sicherheitslücken in den meisten Webanwendungen, die vermieden werden muss.

Anstatt die Theorie von XSS-Attacken und Techniken zu deren Vermeidung vor dem Beginn der Webanwendungsentwicklung zu erlernen, können Sie diese [sichere Starteranwendung](https://github.com/IBM-Cloud/java-secure-app) verwenden. Die sichere Starteranwendung enthält Codebeispiele aus der Programmierpraxis für Schlüsselsicherheit, die XSS vermeiden, sodass Sie mit der Entwicklung beginnen können, während Sie Techniken zur Vermeidung von XSS erlernen und anwenden.

## So verwenden Sie die Beispielapp für Sicherheit
{: #how}

Sie können die [sichere Starteranwendung](https://github.com/IBM-Cloud/java-secure-app) als Startpunkt für die neue Liberty-Anwendungsentwicklung verwenden. Beginnen Sie damit, den Code für die XSS-Gegenmaßnahmen in der App nachzuvollziehen und wenden Sie diesen dann auf die Operationen der Anwendungs-API an. Die Gegenmaßnahmen in der sicheren Starteranwendung verhindern, dass böswillige Benutzereingaben Ihre Anwendung auf dem Server und auf dem Browser beschädigen. Dies erfolgt durch die Migration oder Verhinderung von XSS-Attacken.

Laden Sie zunächst die sichere Starteranwendung herunter, erstellen Sie dann einen Build und stellen Sie das Ergebnis unter {{site.data.keyword.Bluemix_notm}} oder lokal auf dieselbe Weise bereit, wie Sie dies mit der Beispielanwendung [getting-started-java](https://github.com/IBM-Cloud/get-started-java) getan haben.  Wechseln Sie zu [Erste Schritte mit Liberty unter {{site.data.keyword.Bluemix_notm}}](getting-started.html), um mehr über die Builderstellung und Bereitstellung von Anwendungen unter {{site.data.keyword.Bluemix_notm}} zu erfahren.  Für den Anfang können Sie diese Schritte verwenden, um die App zu klonen, einen Build zu erstellen und sie auszuführen.

```
git clone https://github.com/IBM-Cloud/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
Die App finden Sie unter http://localhost:9080/GetStartedSecureJava/

## HTTPS auf allen Seiten in Ihrer Anwendung erzwingen
{: #enforce_https}

Wenn auf allen Seiten Ihrer Anwendung HTTPS anstatt HTTP erzwungen werden soll, müssen Sie die folgenden Änderungen vornehmen.

Ändern Sie die Datei 'server.xml', um das `appSecurity-2.0`-Feature zu aktivieren:

```
  <featureManager>
    <feature>appSecurity-2.0</feature>
  </featureManager>
```

Ändern Sie die Datei 'web.xml', um die folgende Integritätsbedingung für die Sicherheit einzubeziehen:

```
  <security-constraint>
    <web-resource-collection>
      <web-resource-name>Entire Application</web-resource-name>
      <url-pattern>/*</url-pattern>
    </web-resource-collection>
    <user-data-constraint>
      <transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
  </security-constraint>
```

Hierdurch erzwingt Ihre Anwendung bei allen Verbindungen die automatische Verwendung von HTTPS und es werden keine HTTP-Verbindungen zugelassen.

## Weitere Informationen
{: more}
Die sichere Starteranwendung enthält **BadServlet.java**. Diese Anwendung zeigt ein Beispiel für unsicheren Code, den Anwendungsentwickler möglicherweise versehentlich schreiben.

Die sichere Starteranwendung enthält außerdem **GoodServlet.java** mit einer Reihe guter und sicherer Beispiele aus der Programmierpraxis wie Eingabevalidierung, Ausgabeverschlüsselung, sichere Einstellungen für HTTP-Header und Sicherheitsrichtlinien für Inhalte (Content Security Policy). Diese Verfahren sind wichtige Maßnahmen gegen XSS. Ihre Anwendung kann auch andere Sicherheitslücken verringern, die durch Injektion und Directory-Traversal-Techniken ausgenutzt werden könnten.

Weitere Informationen über XSS und Gegenmaßnahmen finden Sie unter [XSS Prevention Cheat Sheet ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.owasp.org/index.php/XSS){: new_window}.
