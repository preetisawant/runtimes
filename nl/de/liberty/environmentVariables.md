---

copyright:
  years: 2015, 2018
lastupdated: "2018-03-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Umgebungsvariablen
{: #environment_variables}

Von Liberty for Java unterstützte Umgebungsvariablen

<table>
<tr>
<th align="left">Umgebungsvariablenname</th>
<th align="left">Beschreibung</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>Zum Aktivieren von [App-Management-Dienstprogrammen](../common/app_mng.html).</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>Zum Installieren von [App-Management-Dienstprogrammen](../common/app_mng.html).</td>
</tr>

<tr>
<td>IBM_LIBERTY_BETA</td>
<td>Zum Aktivieren von [Liberty-Beta-Features](usingBetaFeatures.html)</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>Zum Festlegen von [Java-Optionen](customizingJRE.html).</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>Zum Konfigurieren der [Informationen zur Position des Dynatrace-Agenten](dynatrace.html#configuring_liberty_app).</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>Zum Konfigurieren der [IBM JRE-Version](customizingJRE.html).</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>Zum Konfigurieren verschiedener Liberty-Laufzeitoptionen, wie z. B. [Features für WAR- oder EAR-Dateien](optionsForPushing.html#stand_alone_apps).</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>Zum Konfigurieren der [OpenJDK-Version](customizingJRE.html)</td>.
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>Zum Inaktivieren der [automatischen Neukonfiguration durch das Framework Spring](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/framework-spring_auto_reconfiguration.md). Zum Inaktivieren legen Sie den Wert auf 'enabled: false' fest. </td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>Zum Festlegen der Protokollierungsebene des Buildpacks. Mögliche Werte: <b>DEBUG</b>, <b>INFO</b> (Standardwert), <b>WARN</b>, <b>ERROR</b> oder <b>FATAL</b>.</td>
</tr>

<tr>
<td>JVM</td>
<td>Zum Auswählen des [JRE-Typs](customizingJRE.html).</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>Zum Festlegen der [JVM-Argumente](customizingJRE.html).</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[Zum Überschreiben der Servicekonfiguration](autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>Zum Festlegen der Proxy-Server-Informationen.</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>Zum Festlegen der Proxy-Server-Informationen.</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>Zum Inaktivieren des Service [auto-configuration](autoConfig.html#opting_out).</td>
</tr>
</table>
{: caption="Tabelle 1. Verfügbare Umgebungsvariablen für Liberty for Java" caption-side="top"}

## Inaktivierte Attribute im Liberty for Java-Buildpack

Es gibt einige Attribute, die durch das Liberty-Buildpack automatisch inaktiviert werden und die Sie nicht überschreiben können. Die folgenden Umgebungsvariablen und Attribute werden inaktiviert.

### Tabelle der inaktivierten Attribute

<table>
<tr>
<th>Inaktiviertes Attribut </th>
<th>Element</th>
</tr>

<tr>
<td>host</td>
<td>httpEndpoint</td>
</tr>

<tr>
<td>httpPort</td>
<td>httpEndpoint</td>
</tr>

<tr>
<td>trustHostHeaderPort</td>
<td>webContainer</td>
</tr>

<tr>
<td>andextractHostHeaderPort</td>
<td>webContainer</td>
</tr>

<tr>
<td>logDirectory</td>
<td>logging</td>
</tr>

<tr>
<td>consoleLogLevel</td>
<td>logging</td>
</tr>

<tr>
<td>enableWelcomePage</td>
<td>httpDispatcher</td>
</tr>
</table>
{: caption="Tabelle 1. Von Liberty for Java inaktivierte Attribute" caption-side="top"}

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Liberty-Laufzeit](index.html)
* [Übersicht über Liberty](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
