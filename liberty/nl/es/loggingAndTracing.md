---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Configurar el registro y el rastreo
{: #logging_tracing}

## Archivos de registro
{: #log_files}

Los registros estándares de Liberty, como `messages.log` o el directorio `ffdc`, están disponibles en {{site.data.keyword.Bluemix}} en el directorio `logs` de cada instancia de aplicación. Se puede acceder a estos registros desde la consola de {{site.data.keyword.Bluemix_notm}} o mediante CLI de Cloud Foundry. Por ejemplo:

* Para acceder a registros recientes para una app, ejecute el mandato siguiente:

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* Para ver el archivo `messages.log` de una app que se ejecuta en un nodo DEA, ejecute el mandato siguiente:

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* Para ver el archivo `messages.log` de una app que se ejecuta en una célula de Diego, ejecute el mandato siguiente:

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

El nivel de registro y otras opciones de rastreo se pueden establecer mediante el archivo de configuración de Liberty. Para obtener más información, consulte [Resolución de problemas de Liberty: registro y rastreo](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html). El rastreo también se puede ajustar en una instancia de aplicación en ejecución utilizando la consola de {{site.data.keyword.Bluemix_notm}}.

## Utilización de las funciones de rastreo y volcado
{: #using_trace_and_dump}

La configuración de rastreo de Liberty se puede ajustar para una aplicación en ejecución directamente desde la consola de {{site.data.keyword.Bluemix_notm}}. La consola también proporciona la posibilidad de solicitar y descargar volcados de hebras y de almacenamiento dinámico. Para ajustar la configuración de rastreo o solicitar un volcado, seleccione una aplicación Liberty en la consola de {{site.data.keyword.Bluemix_notm}} y elija el menú `Runtime` de la navegación. En la vista `Tiempo de ejecución`, seleccione una instancia y pulse el botón *RASTREO* o *VOLCADO*. Si el ajuste se realiza a nivel de rastreo, consulte [Resolución de problemas de Liberty: registro y rastreo](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html) para obtener detalles de la sintaxis de la especificación de rastreo.

### Cambiar configuración de rastreo a través de SSH en Diego

Para una aplicación Liberty que se ejecuta en una célula de Diego, puede cambiar la configuración de rastreo a través de la CLI de Cloud Foundry utilizando la característica SSH.

La aplicación push debe incluir un archivo server.xml que contenga **updateTrigger** con el valor **polled**, así el entorno de ejecución detectará y aplicará los cambios en la especificación de rastreo en el archivo server.xml.

Consulte en [Enviar por push apps de Liberty con server.xml](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing) opciones para impulsar apps de Liberty con server.xml

Consulte [Control de actualizaciones dinámicas](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window} para obtener información sobre cómo configurar la actualización dinámica en el archivo server.xml.

Para cambiar la configuración de rastreo, siga estos pasos:

1. SSH para su app

  ```
$ cf ssh <appname> [-i instance_index]
  ```
  {: pre}

2. Edite ```<logging traceSpecification="xxxx"/>``` en server.xml para definir la especificación de rastreo que desea, por ejemplo mediante *vi*:

  ```
$ vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: pre}

Nota: el cambio en server.xml se perderá al volver a transferir o reiniciar, y sólo es válido para la instancia en la que hace ssh.

Consulte [Resolución de problemas de Liberty: registro y rastreo](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window} para obtener detalles sobre la sintaxis de la especificación de rastreo.

### Activación de volcados mediante SSH en Diego

Para una aplicación que se ejecuta en una célula de Diego, puede activar un volcado de hebras y de almacenamiento dinámico mediante la CLI CF utilizando la característica SSH. Por ejemplo:

  ```
$ cf ssh <appname> -c "pkill -3 java"
  ```
  {: pre}

Consulte la documentación siguiente para obtener detalles sobre cómo descargar los archivos de volcado generados.

## Descargue archivos de volcado
{: #download_dumps}

De forma predeterminada, los diversos archivos de volcado se colocan en el directorio `dumps` del contenedor de la aplicación.

### Aplicación DEA

Para una aplicación que se ejecuta en un nodo DEA, utilice la función "cf files" para ver y descargar los archivos de volcado.

* Para ver los volcados generados, ejecute el siguiente mandato:

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* Para descargar un archivo de volcado, ejecute los mandatos siguientes:

    1. Obtenga el GUID de la aplicación

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. Descargue el archivo de volcado

      ```
      $ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
      ```
      {: codeblock}

### Aplicación Diego

Para una aplicación que se ejecuta en una célula de Diego, utilice la función "cf ssh" para ver y descargar los archivos de volcado.

* Para ver los volcados generados, ejecute el siguiente mandato:

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Para descargar un archivo de volcado, ejecute el mandato siguiente:

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

También se puede utilizar `scp` y otras herramientas similares para ver y descargar los archivos de volcado. Consulte el apartado sobre [Acceso a apps con SSH  ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) para obtener más información.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general de Liberty](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
