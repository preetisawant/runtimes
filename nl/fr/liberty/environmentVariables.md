---

copyright:
  years: 2015, 2019
lastupdated: "2018-02-01"
subcollection: "liberty"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Variables d'environnement
{: #environment_variables}

Variables d'environnement prises en charge par Liberty for Java.

<table>
<tr>
<th align="left">Nom de la variable d'environnement</th>
<th align="left">Description</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>Activer les [utilitaires de gestion des applications](/docs/runtimes-common/app_mng.html)</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>Installer les [utilitaires de gestion des applications](/docs/runtimes-common/app_mng.html)</td>
</tr>

<tr>
<td>IBM_LIBERTY_MONTHLY</td>
<td>Activer l'[exécution de l'édition mensuelle de Liberty](/docs/runtimes/liberty/usingMonthlyRuntime.html)</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>Définir les [options Java](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>Configurer les [informations d'emplacement d'agent Dynatrace](/docs/runtimes/liberty/monitoring/dynatrace.html#configuring_liberty_app)</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>Configurer la [version d'IBM JRE](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>Configurer diverses options d'environnement d'exécution Liberty, notamment des [fonctions pour les fichiers WAR ou EAR](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>Configurer la [version d'OpenJDK](/docs/runtimes/liberty/customizingJRE.html).</td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>Désactiver l'[infrastructure de reconfiguration automatique Spring](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/framework-spring_auto_reconfiguration.md). Pour la désactiver, définir la valeur enabled: false. </td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>Définir le niveau de journalisation du pack de construction. Les valeurs possibles sont les suivantes : <b>DEBUG</b>, <b>INFO</b> (par défaut), <b>WARN</b>, <b>ERROR</b> ou <b>FATAL</b></td>
</tr>

<tr>
<td>JVM</td>
<td>Sélectionner le [type d'environnement d'exécution Java](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>Définir les [arguments JVM](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[Remplacer la configuration de service](/docs/runtimes/liberty/autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>Définir les informations relatives au serveur proxy</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>Définir les informations relatives au serveur proxy</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>Désactiver la [configuration automatique](/docs/runtimes/liberty/autoConfig.html#opting_out) des services</td>
</tr>
</table>
{: caption="Tableau 1. Variables d'environnement disponibles pour Liberty for Java" caption-side="top"}

## Attributs désactivés dans le pack de construction Liberty for Java

Certains attributs sont automatiquement désactivés par le pack de construction Liberty et vous ne pouvez pas les redéfinir. Les variables d'environnement et attributs suivants sont désactivés.

### Tableau des attributs désactivés

<table>
<tr>
<th>Attribut désactivé </th>
<th>Élément</th>
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
{: caption="Tableau 1. Attributs désactivés par Liberty for Java" caption-side="top"}
