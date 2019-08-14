---

copyright:
  years: 2015, 2019
lastupdated: "2018-02-01"
subcollection: "liberty"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Variables de entorno
{: #environment_variables}

Variables de entorno admitidas por Liberty para Java.

<table>
<tr>
<th align="left">Nombre de la variable de entorno</th>
<th align="left">Descripción</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>Habilitar [Utilidades de App Management](/docs/runtimes-common/app_mng.html)</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>Instalar [Utilidades de App Management](/docs/runtimes-common/app_mng.html)</td>
</tr>

<tr>
<td>IBM_LIBERTY_MONTHLY</td>
<td>Habilitar [tiempo de ejecución de release mensual de Liberty/](/docs/runtimes/liberty/usingMonthlyRuntime.html)</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>Establecer [Opciones de Java](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>Configurar la [información sobre ubicación del agente de Dynatrace](/docs/runtimes/liberty/monitoring/dynatrace.html#configuring_liberty_app)</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>Configurar la [versión de IBM JRE](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>Configurar una variedad de opciones de tiempo de ejecución de Liberty incluidas las [características para archivos WAR o EAR](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>Configurar la [versión de OpenJDK](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>Inhabilite el [marco de Spring Auto-Reconfiguration](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/framework-spring_auto_reconfiguration.md). Para inhabilitarla, establezca el valor en enabled: false. </td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>Establecer nivel de registro del paquete de compilación. Valores posibles: <b>DEBUG</b>, <b>INFO</b> (valor predeterminado), <b>WARN</b>, <b>ERROR</b>, o <b>MUY GRAVE</b></td>
</tr>

<tr>
<td>JVM</td>
<td>Seleccionar el [Tipo de JRE](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>Establecer los [argumentos de JVM](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[Sustituir configuración de servicio](/docs/runtimes/liberty/autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>Establecer la información del servidor proxy</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>Establecer la información del servidor proxy</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>Inhabilitar el servicio de [autoconfiguración.](/docs/runtimes/liberty/autoConfig.html#opting_out)</td>
</tr>
</table>
{: caption="Tabla 1. Variables de entorno disponibles para Liberty for Java" caption-side="top"}

## Atributos inhabilitados en el paquete de compilación de Liberty for Java

Existen algunos atributos inhabilitados automáticamente por el paquete de compilación de Liberty, que no puede alterar temporalmente. Las siguientes variables de entorno y atributos están inhabilitados.

### Tabla de atributos inhabilitada

<table>
<tr>
<th>Atributo inhabilitado </th>
<th>Elemento</th>
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
{: caption="Tabla 1. Atributos inhabilitados por Liberty for Java" caption-side="top"}
