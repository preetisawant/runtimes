---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-14"

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

* {: download} Enhorabuena, ha desplegado una aplicación de ejemplo Hello World en {{site.data.keyword.Bluemix}}.  Para empezar a trabajar, siga los pasos de esta guía. O bien <a class="xref" href="http://bluemix.net" target="_blank" title="(Descargue el código de ejemplo)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Descargue el código de aplicación" />descargue el código de ejemplo</a> y explore por su cuenta.

Si sigue esta guía de aprendizaje, configurará un entorno de desarrollo, desplegará una app localmente y en {{site.data.keyword.Bluemix}} e integrará un servicio de base de datos de {{site.data.keyword.Bluemix_notm}} en su app.

## Antes de empezar
{: #prereqs}
* [Git ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git-scm.com/downloads){: new_window}
* [CLI de Cloud Foundry ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Compilador de Swift ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://swift.org/download/) para su plataforma.

## Paso 1: Clone la app de ejemplo
{: #clone}

Ahora está listo para empezar a trabar con la app Swift sencilla. Clone el repositorio y vaya al directorio donde se encuentra la app de ejemplo.
  ```
git clone https://github.com/IBM-Bluemix/get-started-swift
  ```
  {: pre}

  ```
cd get-started-swift
  ```
  {: pre}

  Lea detenidamente los archivos del directorio *get-started-swift* para familiarizarse con el contenido.

## Paso 2: Ejecute la app localmente
{: #run_locally}

Cuando haya instalado el compilador de Swift y clonado el repositorio Git, podrá compilar y ejecutar la aplicación. Vaya al directorio raíz de este repositorio en el sistema y emita el siguiente mandato:
```
swift build
```
{: pre}

Este mandato puede tardar unos minutos en ejecutarse.

Cuando la aplicación se haya compilado correctamente, podrá ejecutar el archivo ejecutable que ha generado el compilador de Swift:
```
.build/debug/get-started-swift
```
{: pre}

Debería ver una salida similar a la siguiente:

```
Server is listening on port: 8080
```
{: codeblock}

Ver la app en http://localhost:8080

## Paso 3: Prepare la app para el despliegue
{: #prepare}

Para desplegar en {{site.data.keyword.Bluemix_notm}}, puede resultarle útil configurar un archivo manifest.yml. El archivo manifest.yml incluye información básica sobre la app, como por ejemplo el nombre, la cantidad de memoria a asignar para cada instancia y la ruta. Encontrará un archivo manifest.yml de ejemplo en el directorio `get-started-swift`.

Abra el archivo manifest.yml y cambie el valor de `name` de `GetStartedSwift` por el nombre de su app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedSwift
     random-route: true
     memory: 256M
     command: kitura-helloworld
     buildpack: swift_buildpack
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
  {: pre}

Sustituya *API-endpoint* en el mandato por un punto final de API de la siguiente lista.

| **Nombre de la región** | **Ubicación geográfica** | **Punto final de la API** |
|-----------------|-------------------------|-------------------|
| Región EE.UU. sur| Dallas, EE.UU.| api.ng.bluemix.net |
|  Región EE.UU este | Washington, DC, EE.UU | api.us-east.bluemix.net |
| Región del Reino Unido| Londres, Inglaterra| api.eu-gb.bluemix.net |
| Región de Sídney| Sídney, Australia | api.au-syd.bluemix.net |
|  Región de Alemania | Frankfurt, Alemania | api.eu-de.bluemix.net |
{: caption="Tabla 1. Lista de regiones de {{site.data.keyword.cloud_notm}}" caption-side="top"}

Inicie una sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}

   ```
 cf login
   ```
   {: pre}

Si no puede iniciar sesión utilizando los mandatos `cf login` o `bx login` porque tiene un ID de usuario federado, utilice los mandatos `cf login --sso` o `bx login --sso` para iniciar sesión con el ID de inicio de sesión único. Consulte [Inicio de sesión con un ID federado](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) para obtener más información.

Desde el directorio *get-started-swift*, envíe por push la app a {{site.data.keyword.Bluemix_notm}}
   ```
 cf push
   ```
   {: pre}

Esto puede tardar un minuto. Si hay algún error en el proceso de despliegue, puede utilizar el mandato `cf logs <Your-App-Name> --recent` para resolver problemas.

Cuando finalice el despliegue, verá un mensaje que indica que la app se está ejecutando.  Visualice la app en el URL que aparece en la salida del mandato push.  También puede emitir el mandato `cf apps` para ver el estado de su app y ver el URL.

## Paso 5: Añada una base de datos
{: #add_database}

A continuación, añadiremos una base de datos NoSQL a esta aplicación y configuraremos la aplicación para que se pueda ejecutar localmente y en {{site.data.keyword.Bluemix_notm}}.

1. En el navegador, inicie una sesión en {{site.data.keyword.Bluemix_notm}} y vaya al panel de control. Seleccione **Crear recurso**.
2. Elija la sección **Datos y análisis** y, a continuación, seleccione **BD Cloudant NoSQL** y cree el servicio.
3. Vaya a la vista de **Conexiones** y seleccione su aplicación y, a continuación a **Crear conexión**.
4. Seleccione **Volver a transferir** cuando se le solicite. {{site.data.keyword.Bluemix_notm}} reiniciará la aplicación y proporcionará las credenciales de base de datos para la aplicación mediante la variable de entorno `VCAP_SERVICES`. Esta variable de entorno sólo está disponible para la aplicación cuando se ejecuta en {{site.data.keyword.Bluemix_notm}}.

Las variables de entorno le permiten separar valores de despliegue del código fuente. Por ejemplo, en lugar codificar una contraseña de base de datos, puede guardarla en una variable de entorno a la que haga referencia en el código fuente. [Más información...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Paso 6: Utilice la base de datos
{: #use_database}

Ahora vamos a actualizar el código local para que apunte a esta base de datos. Cree un archivo json que contendrá las credenciales para los servicios que utilizará la aplicación. Este archivo SOLO se utilizará cuando la aplicación se ejecute localmente. Cuando se ejecute en {{site.data.keyword.Bluemix_notm}}, las credenciales se leerán de la variable de entorno VCAP_SERVICES.

Cree un archivo denominado `my-cloudant-credentials.json` en el directorio `config` con el contenido siguiente (como referencia, consulte `config/my-cloudant-credentials.json.example`):

 ```
 {
   "password": "<password>",
   "url": "<url>",
   "username": "<username>"
 }
 ```

Actualice el archivo `mappings.json` en el directorio `config` reemplazando el marcador `cloudant` con el **nombre** de la instancia de BD:

```
{
  "MyCloudantDB": {
    "searchPatterns": [
      "cloudfoundry:cloudant",
      "env:kube-cloudant-credentials",
      "file:config/my-cloudant-credentials.json"
    ]
  }
}
```

Esta aplicación de ejemplo utiliza el paquete `CloudEnvironment` para interactuar con {{site.data.keyword.Bluemix_notm}} y analizar variables de entorno.[Más información...](https://packagecatalog.com/package/IBM-Swift/CloudEnvironment)

El marcador `cloudant` de la configuración `cloudfoundry:cloudant` facilita el enlace a un servicio de Cloudant proporcionado por el usuario para la aplicación.Con la configuración `cloudfoundry:cloudant`, también puede crear un servicio Cloudant que incluya la serie y `cloudant` en algún lugar del nombre de servicio, y enlazarlos a la aplicación, sin editar el archivo `config.json`. Si modifica esta configuración y posteriormente desea utilizar un servicio Cloudant proporcionado por el usuario, necesitará editar la configuración a `cloudfoundry:cloudant` o definir `cloudfoundry:` con el nombre del servicio proporcionado por el usuario.
{: tip}

En la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, seleccione App -> Conexiones -> Cloudant -> Ver credenciales

Copie y pegue sólo las credenciales en los campos correspondientes en el archivo config.json local.

Compile y ejecute la aplicación localmente.
 ```
swift build  
 ```
 {: pre}

  ```
.build/debug/kitura-helloworld
 ```
 {: pre}

Visualice la app en: http://localhost:8080. Cualquier nombre que especifique en la app se añadirá ahora a la base de datos.

 Esta aplicación de ejemplo utiliza el paquete 'Kitura-CouchDB' para interactuar con Cloudant. [Más información... ] (https://packagecatalog.com/package/IBM-Swift/Kitura-CouchDB)

 Realice los cambios que desee y vuelva a desplegarlo en {{site.data.keyword.Bluemix_notm}}!

 ```
 cf app push
 ```

 Visualice la app en el URL que aparece en la salida del mandato push, por ejemplo, *myUrl.mybluemix.net*.
Recuerde que, si no necesita la app en directo, debe detenerla para no incurrir en cargos inesperado.
{: tip}

## Siguientes pasos

* [Guías de aprendizaje](/docs/tutorials/index.html)
* [Ejemplos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://ibm-cloud.github.io){: new_window}
* [Centro de arquitectura![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
