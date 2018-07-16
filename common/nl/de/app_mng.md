---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-02"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Liberty- und Node.js-Apps verwalten
{: #app_management}


App-Management ist eine Reihe von Entwicklungs- und Debugging-Dienstprogrammen, die für Ihre Liberty- und Node.js-Anwendungen in {{site.data.keyword.Bluemix}} aktiviert werden können.
{:shortdesc}

## App-Management-Dienstprogramme
{: #Utilities}


### Dienstprogramme für sowohl Liberty als auch Node.js
* [proxy](#proxy)
* [noproxy](#noproxy)
* [devconsole](#devconsole)
* [hc](#hc)
* [shell](#shell)

### Dienstprogramme für Liberty
* [debug](#debug)
* [jmx](#jmx)
* [localjmx](#localjmx)

### Dienstprogramme für Node.js
* [inspector](#inspector)
* [trace](#trace)

## So konfigurieren Sie App-Management
{: #configure}
Zum Aktivieren der App-Management-Dienstprogramme setzen Sie den Wert der Umgebungsvariablen *BLUEMIX_APP_MGMT_ENABLE* auf das Dienstprogramm oder die Liste von Dienstprogrammen, die aktiviert werden sollen, und führen anschließend ein erneutes Staging für Ihre Anwendung durch. Sie können mehrere Dienstprogramme aktivieren, indem Sie die durch ein **+** trennen.

Führen Sie beispielsweise den folgenden Befehl aus, um die Dienstprogramme *hc*, *debug* und *trace* zu aktivieren:

```
ibmcloud cf set-env myApp BLUEMIX_APP_MGMT_ENABLE hc+debug+trace
```
{: codeblock}

Führen Sie nach dem Einstellen der Umgebungsvariablen ein erneutes Staging für Ihre Anwendung aus:

```
ibmcloud cf restage myApp
```
{: codeblock}

Wenn die App-Management-Dienstprogramme nicht mit Ihren Anwendungen installiert werden sollen, setzen Sie die Umgebungsvariable *BLUEMIX_APP_MGMT_INSTALL* auf 'false' und führen ein erneutes Staging für Ihre Anwendung durch.

Führen Sie z. B. die folgenden Befehle aus, um für Ihre Anwendung ein Staging ohne App-Management-Dienstprogramme durchzuführen:

```
ibmcloud cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
ibmcloud cf restage myApp
```
{: codeblock}

## Einschränkungen
{: #restrictions}
* Änderungen, die Sie mithilfe von App-Management an Ihrer Anwendung vornehmen, sind transient und gehen verloren, wenn Sie diesen Modus verlassen. Dieser Modus ist nur für die temporäre Entwicklung gedacht und sollte aus Leistungsgründen nicht als Produktionsumgebung verwendet werden.
* Bei Node.js-Anwendungen funktionieren die meisten App-Management-Dienstprogramme nicht, wenn Sie den Befehl **start** in der Datei `manifest.yml` oder mit der Option `-c` über die Befehlszeile angeben. Mit diesen Methoden wird das Buildpack außer Kraft gesetzt. Sie sind Antimuster für das Starten von Node.js-Anwendungen. Die besten Ergebnisse erzielen Sie, wenn Sie den Befehl **start** in die Datei `package.json` oder `Procfile` einfügen.

### Dienstprogramme für Liberty und Node.js
{: #liberty_and_node_utilities}

#### proxy
{: #proxy}

Das Dienstprogramm *proxy* stellt minimales Anwendungsmanagement zwischen Ihrer Anwendung und {{site.data.keyword.Bluemix_notm}} bereit.

Wenn es aktiviert ist, startet das Buildpack einen Proxy-Agenten, der sich zwischen der Laufzeit und dem Container der Anwendung befindet.  Das Dienstprogramm *proxy* verarbeitet alle Anforderungen, die die Anwendung empfängt. Je nach dem Typ der Anforderung wird entweder eine App-Management-Aktion ausgeführt oder die Anforderung an die Anwendung weitergeleitet. Bei Verwendung von *proxy* bleibt der Anwendungscontainer auch dann bestehen, wenn die Anwendung ausfällt. Der Proxy-Agent unterstützt auch inkrementelle Dateiaktualisierungen, wodurch der Modus *Live Edit* für Node.js-Anwendungen ermöglicht wird.

Für einige App-Management-Dienstprogramme muss das Dienstprogramm *proxy* mit der Anwendung verwendet werden. Sie können *proxy* automatisch starten.

#### noproxy
{: #noproxy}

Mit dem Dienstprogramm *noproxy* wird das Dienstprogramm *proxy* inaktiviert, wenn es von einem anderen Dienstprogramm automatisch gestartet wurde.  Mit Diego ist der Proxy nicht erforderlich, da Diego die Möglichkeit bietet, mit *ssh* direkt auf Ihre Anwendung zuzugreifen und Portweiterleitung einzurichten.

Das Dienstprogramm *noproxy* ist nur für Anwendungen anwendbar, die in einer Diego-Zelle ausgeführt werden.

#### devconsole
{: #devconsole}

Benutzer können mit dem Dienstprogramm für die Entwicklungskonsole (*devconsole*) ihre Anwendungen erneut starten, stoppen oder aussetzen. Benutzer können mit *devconsole* außerdem die Shell aktivieren bzw. auf die Shell zugreifen und das Programm 'inspector' für Dienstprogramme ausführen.  Mit der folgenden URL können Sie auf *devconsole* zugreifen:
```
  https://<yourappname>.mybluemix.net/bluemix-debug/manage
```
{: codeblock}

Für Node-Versionen ab 6.3.0 stellt die Entwicklungskonsole eine Neustartschaltfläche für die Anwendung und Zugriff auf das Dienstprogramm *shell* zur Verfügung.  Weitere Informationen finden Sie in der Beschreibung zu *inspector*.

**Wichtig**: Das Dienstprogramm *devconsole* startet *proxy*.

#### hc
{: #hc}

Der Health Center-Agent (*hc*) sorgt dafür, dass Ihre Anwendung mit dem Health Center-Client überwacht werden kann.  Für Node.js ist der Agent *hc* nur bei den Node.js-Laufzeitversionen verfügbar, die im IBM SDK for Node.js-Buildpack enthalten sind.  Die aktuelle Gruppe der Laufzeiten finden Sie in [Neueste Aktualisierungen für das SDK for Node.js-Buildpack](/docs/runtimes/nodejs/updates.html).

Wenn der Health Center-Agent aktiviert ist, können Sie die Leistung Ihrer Liberty- und Node.js-Anwendungen mithilfe der IBM Monitoring and Diagnostic Tools analysieren. Weitere Informationen finden Sie in [So analysieren Sie die Leistung von Liberty Java- oder Node.js-Apps in {{site.data.keyword.Bluemix_notm}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}.

**Wichtig:** Das Dienstprogramm *hc* startet *proxy*.

***hc* mit *noproxy* verwenden**

Das Dienstprogramm *hc* kann zusammen mit *noproxy* verwendet werden. Soll Health Center mit *noproxy* verwendet werden, richten Sie zunächst mit dem Befehl `ibmcloud cf ssh` die Portweiterleitung ein. Beispiel:

```
ibmcloud cf ssh -N -T -L 1883:127.0.0.1:1883 <appName>
```
{: codeblock}

Anschließend müssen Sie eine Verbindung zum Health Center-Client herstellen. Verwenden Sie dazu eine [MQTT-Verbindung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/support/knowledgecenter/SS3KLZ/com.ibm.java.diagnostics.healthcenter.doc/topics/connectingtojvm.html){: new_window} und geben Sie `127.0.0.1` für den Host und `1883` für den Port an.

#### shell
{: #shell}

Das Dienstprogramm *shell* aktiviert eine webbasierte Shell.  Auf *shell* können Sie vom Dienstprogramm *devconsole* aus oder mit der folgenden URL zugreifen:

```
  https://<yourappname>.mybluemix.net/bluemix-debug/shell
```
{: codeblock}

Nachdem Sie auf das Dienstprogramm *shell* zugegriffen haben, wird ein Terminalfenster mit Shellzugriff auf Ihre Anwendung angezeigt. Sie können alle Aktionen ausführen, die in einer regulären Shell unterstützt werden, wie Dateien bearbeiten, die Speichernutzung überprüfen oder Diagnosebefehle ausführen.

**Wichtig:** Das Dienstprogramm *shell* startet auch *proxy*.

Diego stellt eine interaktive Shell über den Befehl `ibmcloud cf ssh` zur Verfügung, daher ist das Dienstprogramm *shell* nur für Anwendungen nützlich, die in einer DEA-Umgebung ausgeführt werden.
{: .tip}


##### Entwicklungsmodus für Eclipse-Tools
{: #devmode}
Der Entwicklungsmodus ist ein Feature der [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html), das Entwicklern die Arbeit mit ihren Anwendungen ermöglicht, während diese in der Cloud ausgeführt werden. Mit dem Entwicklungsmodus in den Eclipse-Tools können Sie Ihre Anwendungen in {{site.data.keyword.cloud_notm}} in einem temporären, sicheren Arbeitsbereich bearbeiten.

Der Entwicklungsmodus wird sowohl für Liberty- als auch Node.js-Anwendungen unterstützt. Wenn der Entwicklungsmodus für Ihre Liberty- oder Node.js-Anwendung aktiviert ist, können Sie Anwendungsdateien stufenweise bearbeiten, ohne dass Sie eine Push-Operation für Ihre Anwendung durchführen müssen. Sie können auch eine Debugsitzung für Ihre Anwendungen erstellen. Der Entwicklungsmodus für Liberty-Anwendungen ist äquivalent zur Aktivierung der App-Management-Dienstprogramme *debug* und *jmx*. Für Node.js-Anwendungen ist er äquivalent zur Aktivierung des Dienstprogramms *inspector*.

### Dienstprogramme für Liberty
{: #liberty_utilities}

#### debug
{: #debug}

Zur Verwendung des Dienstprogramms *debug* müssen Sie die [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html) installieren.

Das Dienstprogramm *debug* versetzt die Liberty-Anwendung in den Debugmodus und ermöglicht Clients wie den IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} die Erstellung einer Sitzung für [fernes Debugging](https://console.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html#remotedebug) mit der Anwendung.

**Wichtig:** Das Dienstprogramm *debug* startet *proxy*.

Das Dienstprogramm *debug* kann zusammen mit *noproxy* verwendet werden. Soll 'debug' mit *noproxy* verwendet werden, richten Sie zunächst mit dem Befehl `ibmcloud cf ssh` die Portweiterleitung ein.

Das folgende Code-Snippet zeigt ein Beispiel für das Format des Befehls `ibmcloud cf ssh`:

```
ibmcloud cf ssh -N -T -L 7777:127.0.0.1:7777 <appName>
```
{: codeblock}

Anschließend müssen Sie in Eclipse eine Verbindung herstellen. Verwenden Sie dazu eine *ferne Java-Konfiguration* und geben Sie für den Host `127.0.0.1` und für den Port `7777` an.

#### jmx
{: #jmx}

Mit dem Dienstprogramm *jmx* kann der JMX-REST-Connector zulassen, dass ein ferner JMX-Client die Anwendung unter Verwendung der {{site.data.keyword.Bluemix_notm}}-Benutzerberechtigungsnachweise verwaltet.

Mit JMX können mehrere Instanzen einer Anwendung überwacht werden; dazu ist jedoch eine separate JMX-Verbindung für jede Instanz erforderlich. Standardmäßig wird die Instanz 0 überwacht. Soll die Instanz 1 überwacht werden, können Sie das folgende Code-Snippet verwenden:

```
ibmcloud cf ssh -i 1 -N -T -L 5000:127.0.0.1:5001
```
{: codeblock}

Weitere Informationen zum Konfigurieren eines JMX-Connectors finden Sie in [Sichere JMX-Verbindung zum Liberty-Profil konfigurieren ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.

**Wichtig**: Das Dienstprogramm *jmx* startet *proxy* nicht.

#### localjmx
{: #localjmx}

Das Dienstprogramm *localjmx* aktiviert das Liberty-Feature [localConnector-1.0 ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feature_localConnector-1.0.html){:new_window}. In Kombination mit der lokalen Portweiterleitung bietet *localjmx* ein alternatives Verfahren, um einem fernen JMX-Client die Verwaltung der Anwendung zu ermöglichen.


**Vorbemerkungen**: Für *localjmx* ist die Installation von JConsole erforderlich.

Das Dienstprogramm *localjmx* ist nur für Anwendungen anwendbar, die in einer Diego-Zelle ausgeführt werden. Zur Verwendung von *localjmx* richten Sie zunächst mit dem Befehl `ibmcloud cf ssh` die Portweiterleitung ein. Beispiel:

```
ibmcloud cf ssh -N -T -L 5000:127.0.0.1:5000 <appName>
```
{: codeblock}

Anschließend müssen Sie eine Verbindung zu JConsole herstellen. Wählen Sie dazu die Option für fernen Prozess**** aus, geben Sie `127.0.0.1:5000` an und verwenden Sie eine unsichere Verbindung.


### Dienstprogramme für Node.js
{: #node_utilities}

#### inspector
{: #inspector}

Mit dem Dienstprogramm 'inspector' können Sie CPU-Auslastungsprofile erstellen, Unterbrechungspunkte hinzufügen und Fehler im Code beheben - und das alles, während Ihre Anwendung in {{site.data.keyword.cloud_notm}} ausgeführt wird.  Für Node.js-Versionen vor 6.3.0 aktiviert 'inspector' die Debuggerschnittstelle von Node Inspector.  Weitere Informationen zu Node Inspector enthält die Readme-Datei für [Node Inspector auf GitHub ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/node-inspector/node-inspector){: new_window}.  Für die Node.js-Versionen 6.3.0 und höher verwendet das Dienstprogramm *inspector* die [V8 Inspector Integration for Node.js ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://nodejs.org/dist/latest-v6.x/docs/api/debugger.html#debugger_v8_inspector_integration_for_node_js){:new_window}.

##### **Für höhere Node.js-Versionen als 6.3.0**
Wenn Sie den Debugmodus starten, wird *proxy* automatisch aktiviert, selbst wenn Sie eine Node.js-Version verwenden, die *proxy* nicht enthält. In höheren Node.js-Versionen als 6.3.0 ist *proxy* nicht enthalten. Wenn Sie das Dienstprogramm *inspector* mit höheren Node.js-Versionen als 6.3.0 verwenden, können Sie *proxy* durch Verwendung von *noproxy* wieder inaktivieren.

Für den Zugriff auf die *inspector*-Schnittstelle können Sie anstelle von *proxy* auch die Funktion 'Developer Tools' des Web-Browsers Google Chrome verwenden.  

Aktivieren Sie mit dem folgenden Befehl den Zugriff auf die URL mit lokaler Portweiterleitung:
```
ibmcloud cf ssh -N -T -L 9229:127.0.0.1:9229 <appName>
```
{: codeblock}

Rufen Sie mit dem folgenden Befehl das Startprotokoll für die Anwendung ab.
```
ibmcloud cf logs <appName> --recent
```
{: codeblock}

Wenn das Dienstprogramm *inspector* aktiv ist, enthält das Protokoll Nachrichten wie die folgenden:
```
 ... Sie benötigen einen SSH-Tunnel für Port 9229, damit Sie mit den Chrome DevTools ein fernes Debugging für Ihre App ausführen können
 ... App wird mit 'node --inspect=9229  app.js ' gestartet
```
{: codeblock}

Navigieren Sie mit einer aktuellen Version des Web-Browsers Google Chrome zu `chrome://inspect`.
Unter dieser URL ist Ihre App zusammen mit einem Link zu Ihren Anwendungsdateien aufgelistet, z. B. `file://home/vcap/app/app.js`. Wählen Sie dann **inspect** aus, um auf die inspect-Schnittstelle zuzugreifen.

##### **Für niedrigere Node.js-Versionen als 6.3.0**
Wenn Sie *proxy* verwenden, können Sie unter `https://myApp.mybluemix.net/bluemix-debug/inspector` auf die *inspector*-Schnittstelle zugreifen.

Wenn Sie das Dienstprogramm *proxy* nicht verwenden, aktivieren Sie den Zugriff auf die Anwendungs-URL, indem Sie die lokale Portweiterleitung mit dem folgendem Befehl verwenden:

```
ibmcloud cf ssh -N -T -L 8790:127.0.0.1:8790 <appName>
```
{: codeblock}

Greifen Sie anschließend von der URL `http://127.0.0.1:8790` aus auf 'inspector' zu.

#### trace (nicht mehr verwendet)
{: #trace}

Mit dem Dienstprogramm 'trace' können Sie dynamisch Tracestufen festlegen, wenn Ihre Anwendung das Protokollierungsmodul log4js, ibmbluemix oder bunyan verwendet.

Navigieren Sie zu der Seite **Instanzdetails** in der {{site.data.keyword.cloud_notm}}-Webkonsole und wählen Sie **Aktionen** aus, um die Benutzerschnittstelle anzuzeigen.

Hinweis: Unterstützte Abhängigkeitsversionen:

* log4js:(0.6.0 - 0.6.24)
* bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
* ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)


Das Dienstprogramm 'trace' ist nicht verfügbar, wenn die Anwendung mit der Option `-b buildpack` gestartet wird.

Das Dienstprogramm 'trace' startet *proxy* nicht.
