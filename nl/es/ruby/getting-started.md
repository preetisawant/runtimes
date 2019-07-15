---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-03"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:aside: .aside}
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
* [Cuenta de {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [CLI de {{site.data.keyword.Bluemix_notm}}](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git-scm.com/downloads){: new_window}
* [Ruby ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ruby-lang.org/en/downloads/){: new_window}
* [rbenv ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/rbenv/rbenv#installation){: new_window}

## Paso 1: Clone la app de ejemplo
{: #clone}

Primero, clone el repositorio y vaya al directorio donde se encuentra la app de ejemplo.

  ```
git clone https://github.com/IBM-Cloud/get-started-ruby
  ```
  {: codeblock}

  ```
cd get-started-ruby
  ```
  {: codeblock}


## Paso 2: Ejecute la app localmente (opcional)
{: #run_locally}

1. Ejecute la app localmente ejecutando los siguientes mandatos.

  ```
rbenv install 2.3.0
  ```
  {: codeblock}

  ```
rbenv local 2.3.0
  ```
  {: codeblock}

  ```
gem install bundler
  ```
  {: codeblock}

  ```
bundle install
  ```
  {: codeblock}

  ```
rails server
  ```
  {: codeblock}

1. Visualice la app en el siguiente URL: http://localhost:3000

## Paso 3: Prepare la app para el despliegue
{: #prepare}

Para desplegar en {{site.data.keyword.Bluemix_notm}}, puede resultarle útil configurar un archivo manifest.yml. El archivo manifest.yml incluye información básica sobre la app, como por ejemplo el nombre, la cantidad de memoria a asignar para cada instancia y la ruta. Encontrará un archivo manifest.yml de ejemplo en el directorio `get-started-ruby`.

Abra el archivo manifest.yml y cambie el valor de `name` de `GetStartedRuby` por el nombre de su app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
applications:
  - name: GetStartedRuby
    random-route: true
    memory: 128M
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

1. Desde el directorio *get-started-node*, envíe por push la app a {{site.data.keyword.Bluemix_short}}.

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

A continuación, añadiremos una base de datos de {{site.data.keyword.cloudant_short_notm}} a esta aplicación y configuraremos la aplicación para que se pueda ejecutar localmente y en {{site.data.keyword.Bluemix_notm}}.

1. En el navegador, inicie una sesión en {{site.data.keyword.Bluemix_notm}} y vaya al panel de control. Seleccione **Crear recurso**.
2. Elija la sección **Datos y análisis** y, a continuación, seleccione **{{site.data.keyword.cloudant_short_notm}}** y cree el servicio.
3. Vaya a la vista de **Conexiones** y seleccione su aplicación y, a continuación a **Crear conexión**.
4. Seleccione **Volver a transferir** cuando se le solicite. {{site.data.keyword.Bluemix_short}} reiniciará la aplicación y proporcionará las credenciales de base de datos para la aplicación mediante la variable de entorno `VCAP_SERVICES`. Esta variable de entorno sólo está disponible para la aplicación cuando se ejecuta en {{site.data.keyword.Bluemix_short}}.

Las variables de entorno le permiten separar valores de despliegue del código fuente. Por ejemplo, en lugar codificar una contraseña de base de datos, puede guardarla en una variable de entorno a la que haga referencia en el código fuente.
{: tip}

## Paso 6: Utilice la base de datos
{: #use_database}
Ahora vamos a actualizar el código local para que apunte a esta base de datos. Crearemos un archivo .env que contendrá las credenciales para los servicios que utilizará la aplicación. Este archivo SOLO se utilizará cuando la aplicación se ejecute localmente. Cuando se ejecute en {{site.data.keyword.Bluemix_notm}}, las credenciales se leerán de la variable de entorno VCAP_SERVICES.

1. Cree un archivo denominado `.env` en el directorio `get-started-ruby` con el contenido siguiente:

  ```
CLOUDANT_URL=
  ```
  {: codeblock}

2. En su navegador, vaya al panel de control de {{site.data.keyword.Bluemix_notm}} y seleccione **_su app_ > Conexiones**. Pulse el icono de menú de {{site.data.keyword.cloudant_short_notm}} (**&vellip;**) y seleccione **Ver credenciales**.

3. Copie y pegue sólo el `url` de las credenciales en el campo `CLOUDANT_URL` del archivo `.env` y guarde los cambios.  El resultado se parecerá al siguiente:

  ```
CLOUDANT_URL=https://123456789 ... bluemix.cloudant.com
  ```
   {: codeblock}

4. Ejecute la aplicación localmente.

  ```
rails server
  ```
  {: codeblock}

  Visualice la app en: http://localhost:3000. Cualquier nombre que especifique en la app se añadirá ahora a la base de datos.

  La app local y la app {{site.data.keyword.Bluemix_notm}} comparten la base de datos.  Visualice la app {{site.data.keyword.Bluemix_notm}} en el URL que aparece en la salida del mandato push anterior.  Los nombres que añada desde cualquiera de las apps deberían aparecer cuando renueve los navegadores.


Si no necesita la app en directo, debe detenerla para no incurrir en cargos inesperado.
{: tip}

## Siguientes pasos

* [Guías de aprendizaje](/docs/tutorials/index.html)
* [Ejemplos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://ibm-cloud.github.io){: new_window}
* [Centro de arquitectura ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
