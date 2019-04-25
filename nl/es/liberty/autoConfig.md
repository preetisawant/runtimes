---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Configurar servicios enlazados
{: #auto_config}

Puede enlazar diversos servicios a su aplicación Liberty for Java. Los servicios se pueden gestionar mediante contenedor, mediante aplicación o ambos, en función de lo que desee el desarrollador.

Un servicio gestionado por la aplicación es un servicio que gestionan por completo la aplicación, sin ayuda de Liberty. La aplicación normalmente lee VCAP_SERVICES para obtener información sobre el servicio enlazado y accede directamente al servicio. La aplicación proporciona todo el código de acceso de cliente necesario. No hay dependencia de las características de Liberty ni de la configuración del archivo `server.xml`. La configuración automática del paquete de compilación de Liberty no se aplica a los servicios de este tipo.

Un servicio gestionado por contenedor es un servicio que está gestionado por el tiempo de ejecución de Liberty. En algunos casos, es posible que la aplicación busque el servicio enlazado en JNDI, mientras que en otros el propio Liberty utiliza directamente el servicio. El paquete de compilación de Liberty lee VCAP_SERVICES para obtener información sobre los servicios enlazados. Para cada servicio gestionado por contenedor, el paquete de compilación lleva a cabo tres funciones.

* Genera [variables de nube](/docs/runtimes/liberty/optionsForPushing.html#accessing_info_of_bound_services) para el servicio enlazado.
* Instala las características de Liberty y el acceso de cliente códigos que son necesarios para acceder al servicio enlazado.
* Genera o actualiza las stanzas del archivo `server.xml` que requiere el servicio.

Este proceso se conoce como configuración automática.

El paquete de compilación de Liberty proporciona configuración automática para los siguientes tipos de servicio:

* [{{site.data.keyword.autoscaling}}](/docs/services/Auto-Scaling/index.html#autoscaling)
* [ClearDB MySQL Database ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.cleardb.com/developers)
* [{{site.data.keyword.cloudant}}](/docs/services/Cloudant/index.html#Cloudant)
* [{{site.data.keyword.composeForMongoDB}}](/docs/services/ComposeForMongoDB/index.html)
* [{{site.data.keyword.composeForMySQL}}](/docs/services/ComposeForMySQL/index.html)
* [{{site.data.keyword.composeForPostgreSQL}}](/docs/services/ComposeForPostgreSQL/index.html)
* [{{site.data.keyword.dashdbshort}}](/docs/services/dashDB/index.html#dashDB)
* [ElephantSQL](/docs/services/ElephantSQL/index.html)
* [{{site.data.keyword.ssoshort}}](/docs/services/SingleSignOn/index.html#sso_gettingstarted)

Los servicios Compose pueden ser gestionados por contenedor o por aplicación. De forma predeterminada, el paquete de compilación de Liberty da por supuesto que estos servicios se gestionan mediante contenedor, y los configura automáticamente. Si desea que la aplicación gestione el servicio, puede renunciar a la configuración automática del servicio estableciendo la variable de entorno. `services_autoconfig_excludes`. Para obtener más información, consulte [Renuncia a la configuración automática del servicio](/docs/runtimes/liberty/autoConfig.html#opting_out).

## Instalación de las características de Liberty y del código de acceso de cliente
{: #installation_of_liberty_features}

Cuando establece un enlace con un servicio gestionado por contenedor, es posible que el servicio necesite que se configuren las características de Liberty en la stanza `featureManager` del archivo `server.xml`. El paquete de compilación de Liberty actualiza la stanza `featureManager` e instala los archivos binarios de soporte necesarios. Si el servicio necesita los archivos JAR del controlador del cliente, los archivos se descargan en una ubicación conocida de la instalación de Liberty.

Consulte la sección [Renuncia a la configuración automática del servicio](#opting_out) para obtener más detalles sobre los tipos de servicio enlazado.

## Generación o actualización de stanzas de configuración de server.xml
{: #generating_or_updating_serverxml}

El paquete de compilación de Liberty puede generar o actualizar automáticamente las stanzas de configuración en el archivo `server.xml` cuando se envía una aplicación autónoma, dependiendo de cómo se enlace la aplicación a los servicios y si ya tiene un archivo `server.xml`.

Cuando envía una aplicación autónoma, el paquete de compilación de Liberty genera la stanza de configuración de `server.xml`, tal como se describe en [Opciones para enviar aplicaciones Liberty](/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing), {{site.data.keyword.Bluemix_notm}}.

Cuando envía una aplicación autónoma y la enlaza a servicios gestionados por contenedor, el paquete de compilación de Liberty genera las stanzas necesarias de `server.xml` para los servicios enlazados.

Cuando se proporciona un archivo `server.xml` y lo enlaza a servicios gestionados por contenedor, el paquete de compilación de Liberty generará o actualizará las stanzas de configuración.

* Si el archivo `server.xml` proporcionado no contiene stanzas de configuración para los servicios en lazados, Liberty genera la configuración para los servicios enlazados.
* Si el archivo `server.xml` proporcionado contiene stanzas de configuración para los servicios enlazados, Liberty actualiza la configuración para los servicios enlazados.

Consulte la documentación del tipo de servicio enlazado para ver más detalles.

## Renuncia a la configuración automática del servicio
{: #opting_out}

En algunos casos, puede que no desee que el paquete de compilación de Liberty configure automáticamente los servicios ha enlazado. Vamos a examinar los casos de ejemplo.

* Mi aplicación utiliza *dashDB*, pero deseo que la aplicación gestione directamente la conexión con la base de datos. La aplicación contiene el archivo JAR de controlador de cliente necesario. No quiero que el paquete de compilación de Liberty configure automáticamente el servicio *dashDB*.
* Estoy proporcionando un archivo `server.xml` y he proporcionado las stanzas de configuración para la instancia *cloudant* porque necesito una configuración de fuente de datos no estándar. No quiero que el paquete de compilación de Liberty actualice mi archivo `server.xml`, pero necesito de todas formas el paquete de compilación de Liberty para asegurarme de que se instala el software de soporte adecuado.

Para renunciar a la configuración automática del servicio, utilice la variable de entorno services_autoconfig_excludes. Puede incluir esta variable de entorno en un archivo manifest.yml o la puede establecer mediante el cliente de {{site.data.keyword.Bluemix_notm}}.

Puede renunciar a la configuración automática de servicios uno por uno. Puede optar por excluir completamente (como en el caso de ejemplo *dashDB*) o renunciar únicamente de las actualizaciones en la configuración del archivo `server.xml` (como en el caso de ejemplo *cloudant*). El valor que especifique para la variable de entorno services_autoconfig_excludes es una serie como se muestra a continuación.

* La serie puede contener especificaciones de renuncia para uno o varios servicios.
* La especificación de renuncia para un servicio específico es service_type=option, donde:
  * service_type es la etiqueta del servicio, tal como se muestra en
VCAP_SERVICES.
  * El valor de option puede ser `all` o `config`.
* Si la serie contiene una especificación de renuncia para más de un servicio,
las especificaciones de renuncia individuales deben ir separadas por un solo carácter de espacio en blanco.

Consulte el ejemplo siguiente de la gramática de la serie `services_autoconfig_excludes`:

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type (service label as it appears in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: codeblock}

**Importante**: El tipo de servicio que especifique debe coincidir con la etiqueta de servicio que aparece en la variable de entorno VCAP_SERVICES. No se permiten espacios en blanco.
**Importante**: No se permiten espacios en blanco en `<service_type_specification>`. Solo se permite el uso de espacios en blanco para separar varias instancias de `<service_type_specification>`.

Utilice la opción **all** para renunciar a todas las acciones de configuración automática para un servicio, como en el caso de ejemplo anterior de *dashDB*. Utilice la opción **configuración** para renunciar únicamente a las acciones de actualización de la configuración como en el caso de ejemplo *cloudant* anterior.

A continuación se muestra un ejemplo de especificaciones de renuncia en un archivo `manifest.yml` para los casos de ejemplo *dashDB* y *cloudant*.

```
    env:
      services_autoconfig_excludes: dashDB=all

    env:
      services_autoconfig_excludes: cloudant=config

    env:
      services_autoconfig_excludes: cloudant=config dashDB=all
```
{: codeblock}

A continuación se muestran ejemplos de cómo establecer la variable de entorno `services_autoconfig_excludes` para la aplicación `myapp` mediante la interfaz de línea de mandatos.

```
    ibmcloud cf set-env myapp services_autoconfig_excludes cloudant=config
    ibmcloud cf set-env myapp services_autoconfig_excludes "cloudant=config dashDB=all"
```
{: codeblock}

Para encontrar la *etiqueta* para un servicio en VCAP_SERVICES emita un mandato como en el siguiente ejemplo:

```
    ibmcloud cf env myapp
```
{: codeblock}

El resultado incluye un texto similar al siguiente, en el que puede ver el campo de `etiqueta` con el valor **elephantsql**:

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

## Sustitución de la configuración de servicio
{: #override_service_config}

En algunos casos, es posible que desee alterar temporalmente la configuración predeterminada para un servicio generado por la configuración automática.
Puede utilizar la variable de entorno **LBP_SERVICE_CONFIG_xxxx** para alterar temporalmente una configuración de servicio. Consulte las siguientes tablas para obtener la sintaxis de ejemplo y nombres de variable de entorno completos para sustituirlos.  Por ejemplo, para sustituir la versión predeterminada del servicio *elephantSQL* y establecerla en la version 8.3.4. + emita un mandato como por ejemplo:

```
    ibmcloud cf set-env myapp LBP_SERVICE_CONFIG_POSTGRESQL "{driver: { version: 8.3.4.+ }}"
```
{: codeblock}

Esta tabla muestra la correlación de **tipo_servicio** con los nombres de variables de entorno **LBP_SERVICE_CONFIG_xxxx**.

<table>
<tr>
<th align="left">service_type</th>
<th align="left">Nombre de la variable de entorno</th>
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


En la tabla siguiente se muestra la sintaxis para sustituir algunas opciones de configuración de servicio:

<table>
<tr>
<th align="left">Nombre de la variable de entorno</th>
<th align="left">Sintaxis de la configuración</th>
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
