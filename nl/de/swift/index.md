---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Cloud Runtime für Swift
{: #swift_runtime}

Die Swift-Laufzeit auf {{site.data.keyword.Bluemix}} wird durch das [{{site.data.keyword.Bluemix_notm}}-Buildpack für Swift](https://github.com/IBM-Swift/swift-buildpack) (swift_buildpack) angetrieben.
Dieses Buildpack bietet eine vollständige Laufzeitumgebung für Swift-Anwendungen.
{: shortdesc}

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} stellt eine auf Kitura basierende Swift-[Starteranwendung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Cloud/Kitura-Starter) bereit. Die Kitura-Starter-App ist eine einfache Swift-App, mit der Sie erfahren können, welche Typen von Serveranwendungen Sie mithilfe der Programmiersprache Swift entwickeln können. Diese Beispielapp erstellt einen Kitura HTTP-Basisserver, der HTML-Inhalte an den Client zurückgibt.

**Hinweis:** Die Kitura-Starter-App ist für Lernzwecke bestimmt. Sie können mit der Starter-App experimentieren, indem Sie Erweiterungen hinzufügen und diese Änderungen mit einer Push-Operation an die {{site.data.keyword.Bluemix_notm}}-Umgebung übertragen. Hilfe zur Verwendung der Starteranwendung finden Sie in [Starteranwendungen verwenden](../common/starter_app_usage.html).

## Ihre App umbenennen
{: #renaming_your_app}

Wenn Sie Ihre App umbenennen möchten (entweder vom Kitura-Starter oder allgemeiner), gibt es einige Änderungen, die berücksichtigt werden müssen. Dadurch werden sowohl Unklarheiten vermieden als auch eine fehlerfreie Bereitstellung sichergestellt.

- Benennen Sie den Projektordner der App um, damit er mit dem Namen Ihrer App übereinstimmt.
- `Package.swift` - Ändern Sie die folgenden Einträge:
    - `name` - Sollte mit dem Namen der App übereinstimmen.
    - `targets[Target(name:)]` - Sollte mit dem Namen der App übereinstimmen.
- `manifest.yml` - Ändern Sie die folgenden Einträge:
    - `name` - Sollte mit dem Namen der App übereinstimmen.
    - `command` - Der Name der ausführbaren Datei, die Ihre App startet (sollte mit dem Namen übereinstimmen, der in der Datei 'Package.swift' angegeben ist).

## Laufzeitversionen
{: #runtime_versions}

Die [Laufzeit für Swift ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Swift/swift-buildpack) (swift_buildpack), die in {{site.data.keyword.Bluemix_notm}} gehostet wird, wurde aktualisiert und verwendet nun die neueste GA-Version der Swift-Binärdateien. Hierbei handelt es sich um die Swift-Version, deren Verwendung in Ihrer App empfohlen wird. In der Datei [manifest.yml ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) des Buildpacks sind auch andere Swift-Versionen aufgeführt, die im Buildpack zwischengespeichert sind, um die Bereitstellungszeit zu reduzieren.

Wenn Sie für Ihre Anwendung eine andere Version von Swift in {{site.data.keyword.Bluemix_notm}} verwenden möchten, können Sie die Version mithilfe einer `.swift-version`-Datei im Stammverzeichnis Ihres Repositorys angeben. Diese `.swift-version`-Datei definiert, welche Swift-Version vom swift_buildpack verwendet werden soll.

```
$ cat .swift-version
4.1.2
```
{: pre}

Da es häufig Aktualisierungen an der Sprache Swift gibt, sollten Sie stets eine `.swift-version`-Datei einbeziehen, damit Ihre App auf die Swift-Version 'fixiert' ist, mit der Ihre Anwendung üblicherweise arbeitet.

Bitte beachten Sie, dass Sie jede gültige Version von Swift in Ihrer `.swift-version`-Datei angeben können. Diese alternativen Versionen müssen mit der Benennung von [Swift.org ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://swift.org/download/) übereinstimmen und werden direkt von dort heruntergeladen. Bei der Verwendung einer Nicht-Cache-Version dauert die Bereitstellung ein wenig länger. Es gibt jedoch keinen Unterschied bei der Laufzeitleistung Ihrer Swift-App.

Das Standardversion von swift_buildpack in {{site.data.keyword.Bluemix_notm}} wird verwendet, wenn das Stammverzeichnis Ihrer App die Datei `Package.swift` enthält.  Falls Sie ein alternatives Buildpack verwenden möchten, müssen Sie dieses durch Hinzufügen eines Eintrags `buildpack: {buildpackUrl}` zu der Datei 'manifest.yml' Ihrer App angeben. Alternativ können Sie dies zum Zeitpunkt der Bereitstellung definieren, indem Sie das Befehlsargument `ibmcloud cf push -b {buildpackUrl}` verwenden.


## Entwicklerumgebungen

Entwickler haben verschiedene Optionen bei der Erstellung von serverseitigen Anwendungen mit Swift. Diejenigen, die Geräte mit Mac OS von Apple verwenden, bevorzugen wahrscheinlich die Verwendung der Xcode-IDE, obwohl dies keine Voraussetzung ist.  Swift-basierte Apps, die unter {{site.data.keyword.Bluemix_notm}} bereitgestellt und ausgeführt werden, können jeden Programmierungseditor und jede IDE verwenden.  Syntaxhervorhebung und Linten stehen für Swift für zahlreiche gängige Editoren zur Verfügung. Das Befehlszeilentool Swift REPL, das in den Binärdateien von [Swift.org ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://swift.org/) enhalten ist, ermöglicht vor der Bereitstellung von {{site.data.keyword.Bluemix_notm}} die lokale Kompilierung und lokale Tests.

Benutzer von Mac OS können die [Kitura-App ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.kitura.io/app.html) verwenden, die die Erstellung, Bereitstellung, Verwaltung und Steuerung serverseitiger Swift-Apps, die in {{site.data.keyword.Bluemix_notm}} ausgeführt werden, vereinfacht.  


## Erweiterte Integration

Die Arbeit mit dem [Kitura-Web-Framework](http://ibm-swift.github.io/Kitura/) bietet eine ganze Reihe von Möglichkeiten. Kitura ist modular aufgebaut und Sie werden sehr bald seine Funktionalität mit gepackten SDKs erweitern wollen, um Features wie Authentifizierung, Zugriff auf Watson-basierte Services und eine breite Palette von Datenbanken zur Verfügung zu haben.  Kitura bietet direkte Unterstützung für zahlreiche Datenbanken, während andere Open-Source-Projekte auch SDKs für viele Datenbankplattformen zur Verfügung stellen. Im Folgenden finden Sie eine nicht vollständige Liste der durch Kitura zur Verfügung gestellten SDKs für die Arbeit mit externen Ressourcen.

- [IBM Watson Developer Cloud Swift SDK ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/watson-developer-cloud/swift-sdk/)
- [SwiftMetrics ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/RuntimeTools/SwiftMetrics)
- [IBM Cloudant und CouchDB ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Swift/Kitura-CouchDB)
- [KituraKit ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Swift/KituraKit)
- [Swift Kuery ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/Swift-Kuery/)
- [Swift Kuery ORM ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/IBM-Swift/Swift-Kuery-ORM)

Weitere Swift-Pakete, die Sie in Ihre Anwendung integrieren können, finden Sie im Abschnitt zu Paketen in [Kitura.io](https://www.kitura.io/packages.html). Pakete können zu einer Swift-Anwendung hinzugefügt werden, indem die Git-URL des Pakets und Versionsdetails in die Datei `Package.swift` der App einbezogen werden. Weitere Details zum Paketmanagement finden Sie im [Abschnitt zum Paketmanager (Package Manager) von Swift.org](https://swift.org/package-manager/).


## Zugehörige Informationen

Es gibt auch andere Online-Tools, die von IBM für Swift-Entwickler zur Verfügung gestellt werden.
- [IBM Swift DevCenter ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/swift/) - Hauptseite für alle IBM Swift-Informationen. Sie können Informationen zu unseren Produktangeboten, Blogs, soziale Ereignisse, Dokumentation und Vieles mehr finden.
- [Kitura.io ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.kitura.io/index.html) - Neuerungen, Beispiele und Ressourcen für die Erstellung von Kitura-Anwendungen.
- [Swift@IBM Slack ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://swift-at-ibm-slack.mybluemix.net/) - In diesen Foren können Sie Fragen stellen und zusammen mit dem Team von Swift@IBM Probleme beheben.
