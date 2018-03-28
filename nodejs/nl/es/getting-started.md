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

Si sigue la guía de aprendizaje de Node.js, configurará un entorno de desarrollo, desplegará una app localmente y en {{site.data.keyword.Bluemix}} e integrará un servicio de base de datos de {{site.data.keyword.Bluemix_notm}} en su app.

## Antes de empezar
{: #prereqs}

Necesitará las siguientes cuentas y herramientas:
* [Cuenta de {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [CLI de Cloud Foundry ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git-scm.com/downloads){: new_window}
* [Node ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://nodejs.org/en/){: new_window}


## Paso 1: Clone la app de ejemplo
{: #clone}

En primer lugar, clone el repositorio GitHub de la app de ejemplo *hello world* de Node.js.
  ```
git clone https://github.com/IBM-Bluemix/get-started-node
  ```
  {: pre}

## Paso 2: Ejecute la app localmente
{: #run_locally}

Utilice el gestor de paquetes npm para instalar las dependencias y ejecutar su app.

1. En la línea de mandatos, vaya al directorio en el que se encuentra la app de ejemplo.
  ```
cd get-started-node
  ```
  {: pre}

1. Instale las dependencias que aparecen en el archivo [package.json ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.npmjs.com/files/package.json) para ejecutar la app localmente.  
  ```
npm install
  ```
  {: pre}

1. Ejecute la app.
  ```
npm start  
  ```
  {: pre}

Puede ver la app en: http://localhost:3000.

Utilice [nodemon](https://nodemon.io/) para reiniciar automáticamente la aplicación después de modificar archivos.
{: tip}


## Paso 3: Prepare la app para el despliegue
{: #prepare}

Para desplegar en {{site.data.keyword.Bluemix_notm}}, puede resultarle útil configurar un archivo manifest.yml. El archivo manifest.yml incluye información básica sobre la app, como por ejemplo el nombre, la cantidad de memoria a asignar para cada instancia y la ruta. Encontrará un archivo manifest.yml de ejemplo en el directorio `get-started-node`.

Abra el archivo manifest.yml y cambie el valor de `name` de `GetStartedNode` por el nombre de su app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

```
applications:
- name: GetStartedNode
  random-route: true
  memory: 128M
```
{: codeblock}

En este archivo manifest.yml, **random-rout: true** genera una ruta aleatoria para la app a fin de evitar que su ruta entre en conflicto con otras.  Si lo desea, puede sustituir **random-route: true** por **host: myChosenHostName**, especificando el nombre de host que elija. [Más información...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## Paso 4: Despliegue la app
{: #deploy}

Puede utilizar la CLI de Cloud Foundry para desplegar apps en {{site.data.keyword.Bluemix_notm}}.

Ejecute el siguiente mandato para definir el punto final de API, sustituyendo el valor _API-endpoint_ por el punto final de API de su región.
   ```
cf api <API-endpoint>
   ```
   {: pre}

   | **Nombre de la región** | **Ubicación geográfica** | **Punto final de la API** |
   |-----------------|-------------------------|-------------------|
   | Región EE.UU. sur| Dallas, EE.UU.| api.ng.bluemix.net |
   |  Región EE.UU este | Washington, DC, EE.UU | api.us-east.bluemix.net |
   | Región del Reino Unido| Londres, Inglaterra| api.eu-gb.bluemix.net |
   | Región de Sídney| Sídney, Australia | api.au-syd.bluemix.net |
   |  Región de Alemania | Frankfurt, Alemania | api.eu-de.bluemix.net |
   {: caption="Tabla 1. Lista de regiones de {{site.data.keyword.cloud_notm}}" caption-side="top"}

Inicie una sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}.

  ```
cf login
  ```
  {: pre}

Si no puede iniciar sesión utilizando los mandatos `cf login` o `bx login` porque tiene un ID de usuario federado, utilice los mandatos `cf login --sso` o `bx login --sso` para iniciar sesión con el ID de inicio de sesión único. Consulte [Inicio de sesión con un ID federado](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) para obtener más información.

Desde el directorio *get-started-node*, envíe por push la app a {{site.data.keyword.Bluemix_notm}}.
  ```
cf push
  ```
  {: pre}

El despliegue de la aplicación puede tardar unos minutos. Cuando finalice el despliegue, verá un mensaje que indica que la app se está ejecutando. Visualice su app en el URL que aparece en la salida del mandato push o bien visualice el estado de despliegue de la app y el URL con el siguiente mandato:
  ```
cf apps
  ```
  {: pre}

Puede resolver errores en el proceso de despliegue mediante el mandato `cf logs <Your-App-Name> --recent`.
{: tip}

## Paso 5: Añada una base de datos
{: #add_database}

A continuación, añadiremos una base de datos Cloudant NoSQL a esta aplicación y configuraremos la aplicación para que se pueda ejecutar localmente y en {{site.data.keyword.Bluemix_notm}}.

1. En el navegador, inicie una sesión en {{site.data.keyword.Bluemix_notm}} y vaya al panel de control. Seleccione **Crear recurso**.
2. Elija la sección **Datos y análisis** y, a continuación, seleccione **BD Cloudant NoSQL** y cree el servicio.
3. Vaya a la vista de **Conexiones** y seleccione su aplicación y, a continuación a **Crear conexión**.
4. Seleccione **Volver a transferir** cuando se le solicite. {{site.data.keyword.Bluemix_notm}} reiniciará la aplicación y proporcionará las credenciales de base de datos para la aplicación mediante la variable de entorno `VCAP_SERVICES`. Esta variable de entorno sólo está disponible para la aplicación cuando se ejecuta en {{site.data.keyword.Bluemix_notm}}.

Las variables de entorno le permiten separar valores de despliegue del código fuente. Por ejemplo, en lugar codificar una contraseña de base de datos, puede guardarla en una variable de entorno a la que haga referencia en el código fuente. [Más información...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Paso 6: Utilice la base de datos
{: #use_database}
Ahora vamos a actualizar el código local para que apunte a esta base de datos. Crearemos un archivo JSON que contendrá las credenciales para los servicios que utilizará la aplicación. Este archivo SOLO se utilizará cuando la aplicación se ejecute localmente. Cuando se ejecute en {{site.data.keyword.Bluemix_notm}}, las credenciales se leerán de la variable de entorno `VCAP_SERVICES`.

1. En el directorio `get-started-node`, cree un archivo llamado `vcap-local.json` con el siguiente contenido:
  ```
  {
    "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "url":"CLOUDANT_DATABASE_URL"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
    }
  }
  ```
  {: codeblock}

2. En su navegador, vaya a {{site.data.keyword.Bluemix_notm}} y seleccione **Apps > _su app_ > Conexiones > Cloudant > Ver credenciales**.

3. Copie y pegue solo el `url` de las credenciales en el campo `url` del archivo `vcap-local.json`, sustituyendo **CLOUDANT_DATABASE_URL**.

4. Ejecute la aplicación localmente
  ```
npm start  
  ```
  {: pre}

  Visualice la app local en: http://localhost:3000. Cualquier nombre que especifique en la app se añadirá ahora a la base de datos.

** Evite problemas**: {{site.data.keyword.Bluemix_notm}} define la variable de entorno PORT cuando la app se ejecuta en la nube. Cuando ejecuta la app localmente, la variable PORT no está definida, de modo que se utiliza 3000 como número de puerto. Consulte [Ejecutar la app localmente](runningLocally.html#hints) para obtener más información.

  La app local y la app {{site.data.keyword.Bluemix_notm}} comparten la base de datos. Los nombres que añada desde cualquiera de las apps aparecerán cuando renueve los navegadores.

Recuerde que si no necesita la app en directo en {{site.data.keyword.Bluemix_notm}}, debe detener la app para no incurrir en cargos inesperados.
{: tip}

## Siguientes pasos

* [Guías de aprendizaje](/docs/tutorials/index.html)
* [Ejemplos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://ibm-cloud.github.io){: new_window}
* [Centro de arquitectura ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
