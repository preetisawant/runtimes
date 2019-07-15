---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Gebundene Services konfigurieren
{: #auto_config}

Sie können verschiedene Services an Ihre Liberty for Java-Anwendung binden. Abhängig von den Vorgaben des Entwicklers können Services containerverwaltet oder anwendungsverwaltet oder beides sein.

Ein anwendungsverwalteter Service ist ein Service, der ohne Unterstützung von Liberty vollständig von der Anwendung verwaltet wird. Die Anwendung liest in der Regel VCAP_SERVICES, um Informationen zu dem gebundenen Service abzurufen, und greift direkt auf den Service zu. Die Anwendung stellt den gesamten erforderlichen Clientzugriffscode bereit. Es besteht keine Abhängigkeit von Liberty-Features oder der Konfiguration der Datei server.xml. Die automatische Konfiguration des Liberty-Buildpacks wird auf Services dieses Typs nicht angewendet.

Ein containerverwalteter Service ist ein Service, der von der Liberty-Laufzeit verwaltet wird. In manchen Fällen kann es vorkommen, dass die Anwendung den gebundenen Service in JNDI sucht, während der Service in anderen Fällen direkt von Liberty selbst genutzt wird. Das Liberty-Buildpack liest VCAP_SERVICES, um Informationen zu den gebundenen Services zu erhalten. Für jeden containerverwalteten Service führt das Buildpack drei Funktionen aus.

* Generieren von [Cloudvariablen](optionsForPushing.html#accessing_info_of_bound_services) für den gebundenen Service.
* Installieren der Liberty-Features und Clientzugriffscodes, die für den Zugriff auf den gebundenen Service erforderlich sind.
* Generieren oder Aktualisieren der Zeilengruppen der Datei server.xml, die für den Service erforderlich sind.

Dieser Prozess wird als automatische Konfiguration bezeichnet.

Das Liberty-Buildpack bietet automatische Konfiguration für die folgenden Servicetypen:

* [Auto-Scaling](/docs/services/Auto-Scaling/index.html#autoscaling)
* [ClearDB MySQL Database ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.cleardb.com/developers)
* [Cloudant NoSQL Database](/docs/services/Cloudant/index.html#Cloudant)
* [Compose for MongoDB](/docs/services/ComposeForMongoDB/index.html)
* [Compose for MySQL](/docs/services/ComposeForMySQL/index.html)
* [Compose for PostgreSQL](/docs/services/ComposeForPostgreSQL/index.html)
* [dashDB](/docs/services/dashDB/index.html#dashDB)
* [ElephantSQL](docs/services/ElephantSQL/index.html)
* [Single Sign On](/docs/services/SingleSignOn/index.html#sso_gettingstarted)

Die Compose-Services können entweder containerverwaltet oder anwendungsverwaltet sein. Das Liberty-Buildpack geht standardmäßig davon aus, dass diese Services containerverwaltet sind, und konfiguriert sie automatisch. Wenn die Anwendung den Service verwalten soll, können Sie die automatische Konfiguration für den Service ausschließen (Opt-out), indem Sie die Umgebungsvariable `services_autoconfig_excludes` definieren. Weitere Informationen finden Sie in [Automatische Konfiguration von Services ausschließen](autoConfig.html#opting_out).

## Installation von Liberty-Features und Clientzugriffscode
{: #installation_of_liberty_features}

Bei der Bindung an einen containerverwalteten Service müssen möglicherweise Liberty-Features in der Zeilengruppe featureManager der Datei server.xml konfiguriert werden. Das Liberty-Buildpack nimmt eine entsprechende Aktualisierung der Zeilengruppe featureManager vor und installiert die erforderlichen unterstützenden Binärdateien. Wenn der Service Clienttreiber-JAR-Dateien benötigt, werden die JAR-Dateien an eine bekannte Position in der Liberty-Installation heruntergeladen.

Weitere Informationen zu den gebundenen Servicetypen finden Sie in [Automatische Konfiguration von Services ausschließen](#opting_out).

## Konfigurationszeilengruppen der Datei server.xml generieren oder aktualisieren
{: #generating_or_updating_serverxml}

Das Liberty-Buildpack kann Konfigurationszeilengruppen in Ihrer Datei server.xml automatisch generieren oder aktualisieren, wenn Sie eine Push-Operation für eine eigenständige Anwendung durchführen. Dieses Verhalten ist davon abhängig, wie Ihre Anwendung an Services gebunden ist und ob eine Datei server.xml vorhanden ist.

Wenn Sie eine eine Push-Operation für eine eigenständige Anwendung durchführen, generiert das Liberty-Buildpack die Konfigurationszeilengruppe in der Datei server.xml gemäß der Beschreibung in [Optionen zur Durchführung von Push-Operationen für Liberty-Anwendungen](optionsForPushing.html#options_for_pushing) zur Übertragung in {{site.data.keyword.Bluemix_notm}}.

Wenn Sie eine eigenständige Anwendung mit einer Push-Operation übertragen und an containerverwaltete Services binden, generiert das Liberty-Buildpack die erforderlichen Zeilengruppen der Datei server.xml für die gebundenen Services.

Wenn Sie eine Datei server.xml bereitstellen und an containerverwaltete Services binden, generiert oder aktualisiert das Liberty-Buildpack die Konfigurationszeilengruppen.

* Wenn die bereitgestellte Datei server.xml keine Konfigurationszeilengruppen für die gebundenen Services enthält, generiert Liberty die Konfiguration für die gebundenen Services.
* Wenn die bereitgestellte Datei server.xml Konfigurationszeilengruppen für die gebundenen Services enthält, aktualisiert Liberty die Konfiguration für die gebundenen Services.

Weitere Einzelheiten finden Sie in der Dokumentation zum gebundenen Servicetyp.

## Automatische Konfiguration von Services ausschließen
{: #opting_out}

In manchen Fällen soll das Liberty-Buildpack die gebundenen Services vielleicht nicht automatisch konfigurieren. Betrachten Sie die folgenden Szenarios:

* Meine Anwendung verwendet *dashDB*, die Verbindung zur Datenbank soll aber von der Anwendung direkt verwaltet werden. Die Anwendung enthält die erforderliche Clienttreiber-JAR-Datei. Das Liberty-Buildpack soll den *dashDB*-Service nicht automatisch konfigurieren.
* Ich stelle eine Datei server.xml bereit und habe die Konfigurationszeilengruppen für die *cloudant*-Instanz bereitgestellt, da ich eine vom Standard abweichende Datenquellenkonfiguration benötige. Das Liberty-Buildpack soll die Datei server.xml zwar nicht aktualisieren, aber dennoch sicherstellen, dass die entsprechende unterstützende Software installiert wird.

Sie können die automatische Servicekonfiguration über die Umgebungsvariable services_autoconfig_excludes ausschließen. Diese Umgebungsvariable kann in eine Datei 'manifest.yml' eingefügt oder mit dem {{site.data.keyword.Bluemix_notm}}-Client definiert werden.

Das Ausschließen der automatischen Konfiguration kann pro Servicetyp erfolgen. Sie können die Konfiguration vollständig ausschließen (wie im *dashDB*-Szenario) oder nur die Konfigurationsaktualisierungen in der Datei server.xml ausschließen (wie im *cloudant*-Szenario). Der Wert, den Sie für die Umgebungsvariable services_autoconfig_excludes angeben, ist eine Zeichenfolge, für die Folgendes gilt:

* Die Zeichenfolge kann Opt-out-Spezifikationen für einen oder mehrere Services enthalten.
* Die Opt-out-Spezifikation für einen bestimmten Service lautet service_type=option'. Dabei gilt Folgendes:
  * 'service_type ist die Bezeichnung für den Service gemäß VCAP_SERVICES.
  * Die Option lautet entweder all oder config'.
* Wenn die Zeichenfolge eine Opt-out-Spezifikation für mehrere Services enthält, müssen die einzelnen Opt-out-Spezifikationen durch ein einzelnes Leerzeichen voneinander getrennt werden.

Im Folgenden ist ein Beispiel für die Grammatik der Zeichenfolge services_autoconfig_excludes aufgeführt:

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type (service label as it appears in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: codeblock}

**Wichtig:** Der angegebene Servicetyp muss mit der in der Umgebungsvariablen VCAP_SERVICES enthaltenen Servicebezeichnung übereinstimmen. Leerzeichen sind nicht zulässig.
**Wichtig:** In `<service_type_specification>` ist kein Leerzeichen zulässig. Leerzeichen dürfen nur verwendet werden, um mehrere Instanzen von `<service_type_specification>` voneinander zu trennen.

Verwenden Sie die Option **all**, um alle automatischen Konfigurationsaktionen für einen Service auszuschließen, wie im obigen *dashDB*-Szenario. Verwenden Sie die Option **config**, um nur die Konfigurationsaktualisierungsaktionen auszuschließen, wie im obigen *cloudant*-Szenario.

Im Folgenden einige Opt-out-Beispielspezifikationen in einer Datei manifest.yml für das *dashDB*- und *cloudant*-Szenario.

```
    env:
      services_autoconfig_excludes: dashDB=all

    env:
      services_autoconfig_excludes: cloudant=config

    env:
      services_autoconfig_excludes: cloudant=config dashDB=all
```
{: codeblock}

Beispiele für die Konfiguration der Umgebungsvariablen services_autoconfig_excludes für die Anwendung myapp über die Befehlszeilenschnittstelle:

```
    ibmcloud cf set-env myapp services_autoconfig_excludes cloudant=config
    ibmcloud cf set-env myapp services_autoconfig_excludes "cloudant=config dashDB=all"
```
{: codeblock}

Zum Suchen von *label* für einen Service in VCAP_SERVICES setzen Sie einen Befehl wie im folgenden Beispiel ab:

```
    ibmcloud cf env myapp
```
{: codeblock}

Die Ausgabe enthält Text wie den folgenden, bei dem das Feld **label** den Wert **elephantsql** enthält:

```
   "elephantsql": [
   {
      "credentials": {
      "max_conns": "5",
      "uri":      "..."
   },
   "label": "elephantsql",

```
{: codeblock}

## Servicekonfiguration überschreiben
{: #override_service_config}

In einigen Fällen ist es möglicherweise sinnvoll, die Standardkonfiguration für einen Service, die von der automatischen Konfiguration erstellt wurde, zu überschreiben.
Sie können die Umgebungsvariable **LBP_SERVICE_CONFIG_xxxx** verwenden, um eine Servicekonfiguration zu überschreiben. In den folgenden Tabellen sind die vollständigen Namen der Umgebungsvariablen und eine Beispielsyntax für ihre Überschreibung aufgeführt.  Soll beispielsweise die Standardversion des Service *elephantSQL* überschrieben und auf die Version 8.3.4.+ gesetzt werden, setzen Sie einen Befehl wie den folgenden ab:

```
    ibmcloud cf set-env myapp LBP_SERVICE_CONFIG_POSTGRESQL "{driver: { version: 8.3.4.+ }}"
```
{: codeblock}

Diese Tabelle zeigt die Zuordnung von **service_type** zu den Namen der Umgebungsvariablen **LBP_SERVICE_CONFIG_xxxx**.

<table>
<tr>
<th align="left">service_type</th>
<th align="left">Umgebungsvariablenname</th>
</tr>

<tr>
<td>Auto-Scaling</td>
<td>LBP_SERVICE_CONFIG_AUTO-SCALING</td>
</tr>

<tr>
<td>cleardb</td>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
</tr>

<tr>
<td>cloudantNoSQLDB</td>
<td>LBP_SERVICE_CONFIG_CLOUDANTNOSQLDB</td>
</tr>

<tr>
<td>compose-for-mongodb</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MONGO</td>
</tr>

<tr>
<td>compose-for-mysql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
</tr>

<tr>
<td>compose-for-postgresql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
</tr>

<tr>
<td>elephantsql</td>
<td>LBP_SERVICE_CONFIG_POSTGRESQL</td>
</tr>

<tr>
<td>SingleSignOn</td>
<td>LBP_SERVICE_CONFIG_SINGLESIGNON</td>
</tr>
</table>


Die folgende Tabelle zeigt die Syntax für das Überschreiben einiger Servicekonfigurationsoptionen:

<table>
<tr>
<th align="left">Umgebungsvariablenname</th>
<th align="left">Konfigurationssyntax</th>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>
</table>



# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
