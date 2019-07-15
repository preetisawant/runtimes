---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Configurar el registro y el rastreo
{: #logging_tracing}

## Archivos de registro
{: #log_files}

Los registros estándares de Liberty, como `messages.log` o el directorio `ffdc`, están disponibles en {{site.data.keyword.Bluemix}} en el directorio `logs` de cada instancia de aplicación. Se puede acceder a estos registros desde la consola de {{site.data.keyword.Bluemix_notm}} o mediante CLI de {{site.data.keyword.Bluemix_notm}}. Por ejemplo:

* Para acceder a registros recientes para una app, ejecute el mandato siguiente:

  ```
  ibmcloud cf logs --recent <appname>
  ```
  {: codeblock}


* Para ver el archivo `messages.log` de una app, ejecute el mandato siguiente:

  ```
  ibmcloud cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

El nivel de registro y otras opciones de rastreo se pueden establecer mediante el archivo de configuración de Liberty. Para obtener más información, consulte [Resolución de problemas de Liberty: registro y rastreo](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html).

## Utilización de las funciones de rastreo y volcado
{: #using_trace_and_dump}

### Utilización de rastreo y volcado en la consola {{site.data.keyword.Bluemix_notm}} (en desuso)

La configuración de rastreo de Liberty se puede ajustar para una aplicación en ejecución directamente desde la consola de {{site.data.keyword.Bluemix_notm}}. La consola también proporciona la posibilidad de solicitar y descargar volcados de hebras y de almacenamiento dinámico. Para ajustar la configuración de rastreo o solicitar un volcado, seleccione una aplicación Liberty en la consola de {{site.data.keyword.Bluemix_notm}} y elija el menú `Runtime` de la navegación. En la vista `Runtime`, seleccione una instancia y pulse el botón *TRACE* o *DUMP*. Si el ajuste se realiza a nivel de rastreo, consulte [Resolución de problemas de Liberty: registro y rastreo](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html) para obtener detalles de la sintaxis de la especificación de rastreo.

### Cambiar configuración de rastreo a través de SSH

Cuando envía por push la aplicación, el archivo server.xml incluye las propiedades predeterminadas  **updateTrigger** establecidas en **polled** y **monitorInterval** establecidas en 1 minuto. El servidor Liberty se configura automáticamente para comprobar las actualizaciones del archivo server.xml cada minuto.

Consulte en [Enviar por push apps de Liberty con server.xml](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing) para encontrar opciones para impulsar apps de Liberty con un archivo `server.xml` personalizado.

Consulte [Control de actualizaciones dinámicas ](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window} para saber cómo configurar la actualización dinámica en el archivo server.xml.

Siga estos pasos para cambiar la configuración de rastreo:

1. SSH para su app

  ```
 ibmcloud cf ssh <appname> [-i instance_index]
  ```
  {: codeblock}

2. Edite `<logging traceSpecification="xxxx"/>` en server.xml para definir la especificación de rastreo que desea, por ejemplo mediante *vi*:

  ```
vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: codeblock}

Nota: el cambio en server.xml se perderá al volver a transferir o reiniciar, y sólo es válido para la instancia en la que hace ssh.

Consulte [Resolución de problemas de Liberty: registro y rastreo](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window} para obtener detalles sobre la sintaxis de la especificación de rastreo.

### Activación de volcados mediante SSH

Utilice el mandato siguiente para activar un volcado de hebras y de almacenamiento dinámico mediante la CLI de {{site.data.keyword.Bluemix_notm}} utilizando la característica SSH:

  ```
 ibmcloud cf ssh <appname> -c "pkill -3 java"
  ```
  {: codeblock}

Consulte la documentación siguiente para obtener detalles sobre cómo descargar los archivos de volcado generados.

## Descargue archivos de volcado
{: #download_dumps}

De forma predeterminada, los diversos archivos de volcado se colocan en el directorio `dumps` del contenedor de la aplicación. Utilice la CLI de {{site.data.keyword.Bluemix_notm}} `ibmcloud cf ssh` para ver y descargar los archivos de volcado.

* Para ver los volcados generados, ejecute el siguiente mandato:

  ```
  ibmcloud cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Para descargar un archivo de volcado, ejecute el mandato siguiente:

  ```
  ibmcloud cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

También se puede utilizar `scp` y otras herramientas similares para ver y descargar los archivos de volcado. Consulte el apartado sobre [Acceso a apps con SSH  ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) para obtener más información.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general de Liberty](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
