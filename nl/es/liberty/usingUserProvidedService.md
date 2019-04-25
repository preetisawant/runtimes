---

copyright:
  years: 2017, 2018
lastupdated: "2018-6-26"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Utilización de un servicio proporcionado por el usuario con Liberty en {{site.data.keyword.cloud_notm}}
{: #using_user_provided}

Cloud Foundry proporciona un mecanismo para conectarse y utilizar servicios que no necesariamente proporciona el entorno de
{{site.data.keyword.Bluemix_notm}} ni tienen por qué estar disponibles con él.
Este recurso son los [Servicios proporcionados por el usuario.](https://docs.cloudfoundry.org/devguide/services/user-provided.html).

Este documento presupone que:
  * tiene algún servicio disponible,
  * puede obtener credenciales para dicho servicio,
y describe los pasos necesarios para conectarse y utilizar el servicio con el ejemplo
de aplicación de muestra Getting-Started-Liberty

Para esta explicación utilizaremos la instancia de CloudantNoSQLDB como servicio de ejemplo,
y crearemos un servicio proporcionado por el usuario para conectarnos a él.

## Paso 1: Enviar por push la aplicación Cómo empezar
{: #follow_getting_started}

Siga los pasos en la [guía de aprendizaje Cómo empezar](/docs/runtimes/liberty/getting-started.html) hasta enviar por push
la aplicación a {{site.data.keyword.Bluemix_notm}}.  Deténgase antes de conectar con la base de datos.

## Paso 2: Cree una instancia de CloudantNoSQLDB
{: #create_cloudantnosqldb}

Siga los pasos de la [guía de aprendizaje Cómo empezar](/docs/runtimes/liberty/getting-started.html) para
crear una instancia de CloudantNoSqLDB

Utilice la opción de visualizar credenciales para copiar las credenciales desde CloudandNoSQLDB. Guarde estas credenciales en un archivo local, como por ejemplo cloudant-creds.

## Paso 3: Cree un servicio proporcionado por el usuario
Para trabajar con la aplicación Cómo empezar, el nombre
del servicio proporcionado por el usuario debe contener
"cloudantNoSQLDB".  La aplicación Cómo empezar está
analizando la variable de servicios VCAP y buscando un
servicio proporcionado por el usuario que contenga "cloudantNoSQLDB".

        ibmcloud cf cups my-cloudantNoSQLDB-ups -p cloudant-creds

## Paso 4: Enlace el servicio proporcionado por el usuario y vuelva a transferir la app
Enlace el servicio proporcionado por el usuario con la aplicación Cómo empezar.

        ibmcloud cf bs GettingStartedLiberty my-cloudantNoSQLDB-ups

        ibmcloud cf restage GettingStartedLiberty

## Paso 5: Confirmar
Navegue hasta la aplicación y confirme que puede
añadir varios nombres al campo 'nombre'.
