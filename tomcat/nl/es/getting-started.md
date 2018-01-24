---

copyright:
  years: 2017
lastupdated: "2017-12-15"

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

Si sigue la guía de aprendizaje de iniciación de Tomcat, configurará un entorno de desarrollo, desplegará una app localmente y en {{site.data.keyword.Bluemix}}, e integrará un servicio de base de datos en la app.

## Antes de empezar
{: #prereqs}

Necesitará lo siguiente:
* [Cuenta de {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [CLI de Cloud Foundry ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git-scm.com/downloads){: new_window}
* [Maven ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat versión 8.0.41 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}


## Paso 1: Clone la app de ejemplo
{: #clone}

Ahora está listo para empezar a trabar con la app Tomcat de ejemplo. Clone el repositorio y vaya al directorio donde se encuentra la app de ejemplo.
```
git clone https://github.com/IBM-Bluemix/get-started-tomcat
```
{: pre}

```
cd get-started-tomcat
```
{: pre}

Lea detenidamente los archivos del directorio *get-started-tomcat* para familiarizarse con el contenido.

## Paso 2: Ejecute la app localmente
{: #run_locally}

Debe instalar las dependencias y compilar un archivo .war según se indica en el archivo pom.xml para ejecutar la app.

Instale las dependencias.

```
mvn clean install  
```
{: pre}


Copie GetStartedTomcat.war del directorio `target` en el directorio `tomcat-install-dir` `webapps`.

Ejecute la app.  
```
<tomcat-install-dir>/bin/startup.bat|.sh
```
{: pre}

Visualice la app en: http://localhost:8080/GetStartedTomcat/

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

En este archivo manifest.yml, **random-rout: true** genera una ruta aleatoria para la app a fin de evitar que su ruta entre en conflicto con otras.  Si lo desea, puede sustituir **random-route: true** por **host: myChosenHostName**, especificando el nombre de host que elija. [Más información...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## Paso 4: Despliegue la app
{: #deploy}

Puede utilizar la CLI de Cloud Foundry para desplegar apps.

Elija el punto final de la API

```
cf api <API-endpoint>
```
{:pre}

Sustituya *API-endpoint* en el mandato por un punto final de API de la siguiente lista.

| **Nombre de la región** | **Ubicación geográfica** | **Punto final de la API** |
|-----------------|-------------------------|-------------------|
| Región EE.UU. sur| Dallas, EE.UU.| api.ng.bluemix.net |
|  Región EE.UU este | Washington, DC, EE.UU | api.us-east.bluemix.net |
| Región del Reino Unido| Londres, Inglaterra| api.eu-gb.bluemix.net |
| Región de Sídney| Sídney, Australia | api.au-syd.bluemix.net |
|  Región de Alemania | Frankfurt, Alemania | api.eu-de.bluemix.net |
{: caption="Tabla 1. Lista de regiones de {{site.data.keyword.cloud_notm}}" caption-side="top"}

Inicie una sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}:

```
cf login
```
{: pre}

Si no puede iniciar sesión utilizando los mandatos `cf login` o `bx login` porque tiene un ID de usuario federado, utilice los mandatos `cf login --sso` o `bx login --sso` para iniciar sesión con el ID de inicio de sesión único. Consulte [Inicio de sesión con un ID federado](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) para obtener más información.

Desde el directorio *get-started-tomcat*, envíe por push la app a {{site.data.keyword.Bluemix_notm}}
```
cf push
```
{: pre}

Esto puede tardar un par de minutos. Si hay algún error en el proceso de despliegue, puede utilizar el mandato `cf logs <Your-App-Name> --recent` para resolver problemas.

Cuando finalice el despliegue, verá un mensaje que indica que la app se está ejecutando.  Visualice la app en el URL que aparece en la salida del mandato push.  También puede emitir el mandato
  ```
cf apps
  ```
  {: pre}
  para ver el estado de su app y ver el URL.

## Paso 5: Añada una base de datos
{: #add_database}

A continuación, añadiremos una base de datos NoSQL a esta aplicación y configuraremos la aplicación para que se pueda ejecutar localmente y en {{site.data.keyword.Bluemix_notm}}.

1. En el navegador, inicie una sesión en {{site.data.keyword.Bluemix_notm}} y vaya al panel de control. Seleccione su aplicación pulsando su nombre en la columna **Nombre**.
2. Pulse **Conexiones** y **Crear conexión**.
3. En la sección **Data & Analytics**, seleccione **BD Cloudant NoSQL** y cree el servicio.
4. Vaya a **Apps > Su App > Conexiones** y seleccione **Conectar existente**.
5. Seleccione **Volver a transferir** cuando se le solicite. {{site.data.keyword.Bluemix_notm}} reiniciará la aplicación y proporcionará las credenciales de base de datos para la aplicación mediante la variable de entorno `VCAP_SERVICES`. Esta variable de entorno sólo está disponible para la aplicación cuando se ejecuta en {{site.data.keyword.Bluemix_notm}}.

Las variables de entorno le permiten separar valores de despliegue del código fuente. Por ejemplo, en lugar codificar una contraseña de base de datos, puede guardarla en una variable de entorno a la que haga referencia en el código fuente. [Más información...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Paso 6: Utilice la base de datos
{: #use_database}

Ahora vamos a actualizar el código local para que apunte a esta base de datos. Guardaremos las credenciales correspondientes a los servicios en un archivo de propiedades. Este archivo SOLO se utilizará cuando la aplicación se ejecute localmente. Cuando se ejecute en {{site.data.keyword.Bluemix_notm}}, las credenciales se leerán de la variable de entorno `VCAP_SERVICES`.

1. En su navegador, vaya a {{site.data.keyword.Bluemix_notm}} y seleccione **Apps > _su app_ > Conexiones > Cloudant > Ver credenciales**.

2. Copie y pegue sólo el `url` de las credenciales en el campo `url` del archivo `cloudant.properties` y guarde los cambios.
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:pre}

3. Reinicie el servidor

Renueve la vista del navegador en http://localhost:8080/GetStartedTomcat/. Cualquier nombre que especifique en la app se añadirá ahora a la base de datos.

  La app local y la app {{site.data.keyword.Bluemix_notm}} comparten la base de datos. Los nombres que añada desde cualquiera de las apps aparecerán cuando renueve los navegadores.


Recuerde que si no necesita la app en directo en {{site.data.keyword.Bluemix_notm}}, debe detener la app para no incurrir en cargos inesperados.
{: tip}  

## Siguientes pasos

* [Guías de aprendizaje](/docs/tutorials/index.html)
* [Ejemplos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://ibm-cloud.github.io){: new_window}
* [Centro de arquitectura ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
