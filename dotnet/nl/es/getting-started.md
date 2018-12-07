---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-30"

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

Si sigue esta guía de aprendizaje de iniciación, configurará un entorno de desarrollo, desplegará una app localmente y en {{site.data.keyword.Bluemix}} e integrará un servicio de base de datos de {{site.data.keyword.Bluemix}} en su app.

## Antes de empezar
{: #prereqs}

Necesitará lo siguiente:
* [Cuenta de {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [CLI de {{site.data.keyword.Bluemix_notm}}](../../cli/reference/ibmcloud/download_cli.html)
* [Git ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git-scm.com/downloads){: new_window}
* Instale .NET Core 2.1.1 SDK 2.1.301 desde el [sitio web de descargas de .NET Core ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.microsoft.com/net/download/core).

## Paso 1: Clone la app de ejemplo
{: #clone}

En primer lugar, clone el repositorio GitHub de la app de ejemplo.
  ```
git clone https://github.com/IBM-Cloud/get-started-aspnet-core
  ```
  {: codeblock}


## Paso 2: Ejecute la app localmente
{: #run_locally}

1. En la línea de mandatos, vaya al directorio en el que se encuentra la app de ejemplo.

  ```
  cd get-started-aspnet-core/src/GetStartedDotnet
  ```
  {: codeblock}

1. Ejecute la app localmente ejecutando los siguientes mandatos.

  ```
dotnet restore
  ```
  {: codeblock}

  ```
dotnet run
  ```
  {: codeblock}

1. Visualice la app en: http://localhost:5000/.

## Paso 3: Prepare la app para el despliegue
{: #prepare}

Para desplegar en {{site.data.keyword.Bluemix_notm}}, puede resultarle útil configurar un archivo manifest.yml. El archivo manifest.yml incluye información básica sobre la app, como por ejemplo el nombre, la cantidad de memoria a asignar para cada instancia y la ruta. Encontrará un archivo manifest.yml de ejemplo en el directorio `get-started-dotnet`.

Abra el archivo manifest.yml y cambie el valor de `name` de `GetStartedDotnet` por el nombre de su app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedDotnet
   random-route: true
   memory: 512M
  ```
  {: codeblock}

En este archivo manifest.yml, **`random-rout: true`** genera una ruta aleatoria para la app a fin de evitar que su ruta entre en conflicto con otras.  Si lo desea, puede sustituir **`random-route: true`** por **`host: myChosenHostName`**, especificando el nombre de host que elija.
{: tip}

## Paso 4: Despliegue la app
{: #deploy}

Puede utilizar la CLI de {{site.data.keyword.Bluemix_notm}} para desplegar apps.

1. Inicie sesión en su cuenta de {{site.data.keyword.Bluemix_notm}} y seleccione un punto final de API.
  ```
ibmcloud login
  ```
  {: codeblock}

  Si tiene un ID de usuario federado, en su lugar utilice el siguiente mandato para iniciar sesión con el ID de inicio de sesión único. Consulte [Inicio de sesión con un ID federado](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) para obtener más información.
 ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Destinado a una org y espacio de Cloud Foundry:
  ```
ibmcloud target --cf
  ```
  {: codeblock}

  Si no tiene una org o un espacio configurado, consulte [Adición de organizaciones y espacios](https://console.bluemix.net/docs/account/orgs_spaces.html).
  {: tip}

1. **Asegúrese de que está en el directorio principal, `get-started-aspnet-core`, para la aplicación** y entonces envíe la aplicación a {{site.data.keyword.Bluemix_notm}}:
  ```
ibmcloud cf push
  ```
  {: codeblock}

  Esto puede tardar un minuto. Si hay algún error en el proceso de despliegue, puede utilizar el mandato `ibmcloud cf logs <Your-App-Name> --recent` para resolver problemas.

Cuando finalice el despliegue, verá un mensaje que indica que la app se está ejecutando.  Visualice la app en el URL que aparece en la salida del mandato push.  También puede emitir el siguiente mandato para ver el estado de su app y ver el URL.
  ```
ibmcloud cf apps
  ```
  {: codeblock}

## Paso 5: Añada una base de datos
{: #add_database}

A continuación, añadiremos una base de datos de {{site.data.keyword.cloudant_short_notm}} NoSQL a esta aplicación y configuraremos la aplicación para que se pueda ejecutar localmente y en {{site.data.keyword.Bluemix_notm}}.

1. En el navegador, inicie una sesión en {{site.data.keyword.Bluemix_notm}} y vaya al panel de control. Seleccione **Crear recurso**.
1. Busque **{{site.data.keyword.cloudant_short_notm}}** y seleccione el servicio.
1. Para **Métodos de autenticación disponibles**, seleccione **Utilizar tanto credenciales antiguas como IAM**. Puede dejar los valores predeterminados para los demás campos. Pulse **Crear** para crear el servicio.
1. En el área de navegación, vaya a **Conexiones**. Seleccione la aplicación y pulse **Crear conexión**.
1. Conéctese a la aplicación utilizando los valores predeterminados y pulse **Conectar y volver a transferir la app**. Luego pulse **Volver a transferir** cuando se le solicite.

   {{site.data.keyword.Bluemix_notm}} reiniciará la aplicación y proporcionará las credenciales de base de datos para la aplicación mediante la variable de entorno `VCAP_SERVICES`. Esta variable de entorno sólo está disponible para la aplicación cuando se ejecuta en {{site.data.keyword.Bluemix_notm}}.

Las variables de entorno le permiten separar valores de despliegue del código fuente. Por ejemplo, en lugar de codificar una contraseña de base de datos, puede almacenarla en una variable de entorno a la que hace referencia en el código fuente.
{: tip}

## Paso 6: Utilice la base de datos localmente
{: #use_database}

Ahora vamos a actualizar el código local para que apunte a esta base de datos. Guardaremos las credenciales correspondientes a los servicios en un archivo JSON. Este archivo SOLO se utilizará cuando la aplicación se ejecute localmente. Cuando se ejecute en {{site.data.keyword.Bluemix_notm}}, las credenciales se leerán de la variable de entorno `VCAP_SERVICES`.

1. En el directorio `src/GetStartedDotnet`, cree un archivo `vcap-local.json`.

1. Copie y pegue el siguiente objeto JSON en el archivo `vcap-local.json` y guarde los cambios.

   ```json
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

1. En su navegador, vaya al panel de control de {{site.data.keyword.Bluemix_notm}} y seleccione **_su app_ > Conexiones**. Pulse el icono de menú de {{site.data.keyword.cloudant_short_notm}} (**&vellip;**) y seleccione **Ver credenciales**.

1. Copie y pegue solo el valor `url` de las credenciales en el campo `url` del archivo `vcap-local.json`, sustituyendo `CLOUDANT_DATABASE_URL`.

1. En el directorio `get-started-aspnet-core/src/GetStartedDotnet`, reinicie la aplicación con el siguiente mandato:

   ```
   dotnet run
   ```
   {: codeblock}

1. Renueve la vista del navegador en http://localhost:5000/. Cualquier nombre que especifique en la app se añadirá ahora a la base de datos.

La app local y la app {{site.data.keyword.Bluemix_notm}} comparten la base de datos.  Visualice la app {{site.data.keyword.Bluemix_notm}} en el URL que aparece en la salida del mandato `ibmcloud cf push`.  Los nombres que añada desde cualquiera de las apps deberían aparecer cuando renueve los navegadores.

Recuerde que, si no necesita la app en directo, debe detenerla para no incurrir en cargos inesperado.
{: tip}

## Siguientes pasos

* [Guías de aprendizaje](/docs/tutorials/index.html)
* [Ejemplos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://ibm-cloud.github.io){: new_window}
* [Centro de arquitectura ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
