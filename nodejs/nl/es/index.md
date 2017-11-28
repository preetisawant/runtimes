---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Node.js
{: #nodejs_runtime}

El tiempo de ejecución de Node.js en {{site.data.keyword.Bluemix}} está basado en el paquete de compilación de sdk-for-nodejs.
El paquete de compilación sdk-for-nodejs proporciona un entorno de ejecución completo para apps Node.js.
{: shortdesc}

El paquete de compilación sdk-for-nodejs se utiliza cuando la aplicación contiene un archivo **package.json** en el directorio raíz.

La aplicación debe escuchar en el puerto que se le asigna mediante la variable de entorno PORT.
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio Node.js.  La aplicación de inicio Node.js es una app Node.js sencilla que proporciona una plantilla que puede utilizar para la app. Puede experimentar con la app de inicio, y realizar y enviar por push cambios al entorno de Bluemix. Consulte [Utilización de las aplicaciones de iniciador](/docs/cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de iniciador.

## App Management
{: #app_management}
{{site.data.keyword.Bluemix}} proporciona un número de programas de utilidad para gestionar y depurar la app de Node.js.  Consulte [Gestión de app](/docs/manageapps/app_mng.html) para ver más detalles.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Node.js ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://nodejs.org)
* [IBM API Connect](https://strongloop.com/)
