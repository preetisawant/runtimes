---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-05"
subcollection: "Tomcat"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Guía de aprendizaje de iniciación
{: #getting_started}

* {: download} Enhorabuena, ha desplegado una aplicación de ejemplo Hello World en {{site.data.keyword.Bluemix}}.  Para empezar a trabajar, siga los pasos de esta guía. O bien <a class="xref" href="http://bluemix.net" target="_blank" title="(Descargue el código de ejemplo)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Descargue el código de aplicación" />descargue el código de ejemplo</a> y explore por su cuenta.

Si sigue esta guía de aprendizaje de iniciación, configurará un entorno de desarrollo, desplegará una app localmente y en {{site.data.keyword.Bluemix}}, e integrará un servicio de base de datos en la app.

A lo largo de estos documentos, las referencias a la CLI de Cloud Foundry se han actualizado ahora a la CLI de {{site.data.keyword.Bluemix_notm}}. La CLI de {{site.data.keyword.Bluemix_notm}} tiene los mismos mandatos de Cloud Foundry familiares, pero con una mejor integración con las cuentas de {{site.data.keyword.Bluemix_notm}} y otros servicios. Obtenga más información sobre cómo empezar con la CLI de {{site.data.keyword.Bluemix_notm}} en esta guía de aprendizaje.
{: tip}

## Antes de empezar
{: #prereqs}

Necesitará lo siguiente:
* [Cuenta de {{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/registration)
* [CLI de {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/ibmcloud/download_cli.html)
* [Git ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git-scm.com/downloads){: new_window}
* [Maven ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat versión 8.0.41 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}


## Paso 1: Clone la app de ejemplo
{: #clone}

Clone el repositorio y vaya al directorio donde se encuentra la app de ejemplo.
  ```
git clone https://github.com/IBM-Cloud/get-started-tomcat
  ```
{: codeblock}

  ```
cd get-started-tomcat
  ```
{: codeblock}

Lea detenidamente los archivos del directorio *get-started-tomcat* para familiarizarse con el contenido.

## Paso 2: Ejecute la app localmente
{: #run_locally}

Debe instalar las dependencias y compilar un archivo .war según se indica en el archivo pom.xml para ejecutar la app.

1. Instale las dependencias.
  ```
mvn clean install  
  ```
  {: codeblock}

1. Copie GetStartedTomcat.war del directorio `target` en el directorio `tomcat-install-dir` `webapps`.

1. Ejecute la app.  
  ```
<tomcat-install-dir>/bin/startup.bat|.sh
  ```
  {: codeblock}

1. Visualice la app en el siguiente URL: http://localhost:8080/GetStartedTomcat/

Utilice `shutdown.bat|.sh` para detener la app.  Es posible que tenga que obtener permiso de ejecución de mandatos.
{: tip}

## Paso 3: Prepare la app para el despliegue en {{site.data.keyword.Bluemix_notm}}
{: #prepare}

Para desplegar en {{site.data.keyword.Bluemix_notm}}, puede resultarle útil configurar un archivo manifest.yml. El archivo manifest.yml incluye información básica sobre la app, como por ejemplo el nombre, la cantidad de memoria a asignar para cada instancia y la ruta. Encontrará un archivo manifest.yml de ejemplo en el directorio `get-started-tomcat`.

Abra el archivo manifest.yml y cambie el valor de `name` de `GetStartedTomcat` por el nombre de su app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/GetStartedTomcat.war
    buildpack: java_buildpack
  ```
  {: codeblock}

En este archivo manifest.yml, **`random-rout: true`** genera una ruta aleatoria para la app a fin de evitar que su ruta entre en conflicto con otras.  Si lo desea, puede sustituir **`random-route: true`** por **`host: myChosenHostName`**, especificando el nombre de host que elija.
{: tip}

## Paso 4: Despliegue la app
{: #deploy}

Puede utilizar la CLI de {{site.data.keyword.Bluemix_short}} para desplegar apps.

1. Inicie sesión en su cuenta de {{site.data.keyword.Bluemix_short}} y seleccione un punto final de API.

  ```
ibmcloud login
  ```
  {: codeblock}

  Si tiene un ID de usuario federado, en su lugar utilice el siguiente mandato para iniciar sesión con el ID de inicio de sesión único. Consulte [Inicio de sesión con un ID federado](/docs/cli/login_federated_id.html) para obtener más información.

  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. A continuación, establezca una org y un espacio de Cloud Foundry:
  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Si no tiene una org o un espacio configurado, consulte [Adición de organizaciones y espacios](/docs/account/orgs_spaces.html).
  {: tip}

1. Desde el directorio *get-started-tomcat*, envíe por push la app a {{site.data.keyword.Bluemix_notm}}

  ```
ibmcloud cf push
  ```
  {: codeblock}

  Esto puede tardar un par de minutos. Si hay algún error en el proceso de despliegue, puede utilizar el mandato `ibmcloud cf logs <Your-App-Name> --recent` para resolver problemas.

Cuando finalice el despliegue, verá un mensaje que indica que la app se está ejecutando.  Visualice la app en el URL que aparece en la salida del mandato push.  También puede emitir el siguiente mandato para ver el estado de su app y ver el URL.

  ```
ibmcloud cf apps
  ```
  {: codeblock}

También puede ir a la [Lista de recursos](https://cloud.ibm.com/resources) de {{site.data.keyword.Bluemix_notm}} para ver su app.

## Paso 5: Añada una base de datos
{: #add_database}

A continuación, añadiremos una base de datos de {{site.data.keyword.cloudant_short_notm}} NoSQL a esta aplicación y configuraremos la aplicación para que se pueda ejecutar localmente y en {{site.data.keyword.Bluemix_notm}}.

1. En el navegador, inicie una sesión en {{site.data.keyword.Bluemix_notm}} y vaya al panel de control. Seleccione **Crear recurso**.
1. Busque **{{site.data.keyword.cloudant_short_notm}}** y seleccione el servicio.
1. Para **Métodos de autenticación disponibles**, seleccione **Utilizar tanto credenciales antiguas como IAM**. Puede dejar los valores predeterminados para los demás campos. Pulse **Crear** para crear el servicio.
1. En el área de navegación, vaya a **Conexiones** y pulse **Crear conexión**. Seleccione su aplicación y pulse **Conectar**.
1. Utilizando los valores predeterminados, pulse en **Conectar y volver a transferir la app** para conectar la base de datos a su aplicación. Pulse en **Volver a transferir** cuando se le solicite.

   {{site.data.keyword.Bluemix_notm}} reiniciará la aplicación y proporcionará las credenciales de base de datos para la aplicación mediante la variable de entorno `VCAP_SERVICES`. Esta variable de entorno sólo está disponible para la aplicación cuando se ejecuta en {{site.data.keyword.Bluemix_notm}}.

Las variables de entorno le permiten separar valores de despliegue del código fuente. Por ejemplo, en lugar de codificar una contraseña de base de datos, puede almacenarla en una variable de entorno a la que hace referencia en el código fuente.
{: tip}

## Paso 6: Utilice la base de datos
{: #use_database}

Ahora vamos a actualizar el código local para que apunte a esta base de datos. Guardaremos las credenciales correspondientes a los servicios en un archivo de propiedades. Este archivo SOLO se utilizará cuando la aplicación se ejecute localmente. Cuando se ejecute en {{site.data.keyword.Bluemix_notm}}, las credenciales se leerán de la variable de entorno `VCAP_SERVICES`.

1. Busque la app en la [Lista de recursos](https://cloud.ibm.com/resources) de {{site.data.keyword.Bluemix_notm}}. En la página de Detalles del servicio de su app, pulse **Conexiones** en la barra lateral. Pulse el icono de menú de {{site.data.keyword.cloudant_short_notm}} (**&hellip;**) y seleccione **Ver credenciales**.

2. Copie y pegue sólo el `url` de las credenciales en el campo `url` del archivo `cloudant.properties` y guarde los cambios.
  ```
cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:codeblock}

3. Reinicie el servidor

Renueve la vista del navegador en http://localhost:8080/GetStartedTomcat/. Cualquier nombre que especifique en la app se añadirá ahora a la base de datos.

  La app local y la app {{site.data.keyword.Bluemix_notm}} comparten la base de datos. Los nombres que añada desde cualquiera de las apps aparecerán cuando renueve los navegadores.


Recuerde que si no necesita la app en directo en {{site.data.keyword.Bluemix_notm}}, debe detener la app para no incurrir en cargos inesperados.
{: tip}  

## Siguientes pasos

* [Guías de aprendizaje](/docs/tutorials/index.html)
* [Ejemplos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://ibm-cloud.github.io){: new_window}
* [Centro de arquitectura ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
