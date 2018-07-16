---

copyright:
  years: 2016, 2018
lastupdated: "2018-01-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Modo fuera de línea para Node.js
{: #offline_mode}

Cuando una aplicación Node.js se envía a {{site.data.keyword.Bluemix}}, el paquete de compilación de SDK for Node.js descargará normalmente artefactos desde recursos externos como módulos de Node desde NPM.  En algunas situaciones, como con [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) y [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), puede personalizar el acceso a sitios externos a {{site.data.keyword.Bluemix_notm}}.  
{: shortdesc}

El paquete de compilación Node.js puede acceder a los siguientes sitios externos. Puede que necesite una *lista blanca* de estos sitios en [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) y [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) {{site.data.keyword.Bluemix_notm}}.

* http://nodejs.org/ se puede utilizar para comprobar las versiones del motor del nodo disponibles.
* https://s3pository.heroku.com se utiliza para recuperar versiones del motor de nodos no incluidas en el paquete de compilación.
*  https://www.npmjs.com/package/npm y https://semver.herokuapp.com se utilizan para recuperar versiones de npm no incluidas en el paquete de compilación.
* https://iojs.org se utiliza para recuperar versiones anteriores de nodos que no están contenidas en el paquete de compilación o que no están disponibles en https://semver.herokuapp.com.
* https://registry.npmjs.org se utiliza para recuperar módulos de nodos como por ejemplo express.

Para minimizar el conjunto de sitios incluidos en la lista blanca, configure las aplicaciones de nodos para utilizar una versión del motor de nodos que esté incluida en el paquete de compilación SDK for Node.js.  Consulte [últimas actualizaciones](./updates.html) para el conjunto de versiones del motor del nodo incluido en el paquete de compilación.  Si configura la aplicación para utilizar estas versiones del motor del nodo, entonces sólo es necesario el sitio https://registry.npmjs.org para descargar módulos.

Tenga en cuenta que cuando se instalan versiones nuevas del paquete de compilación SDK for Node.js. el conjunto de versiones del motor de nodos disponible suele cambiar a versiones más recientes.  Puede ser necesario volver a su app para especificar una versión más reciente del motor del nodo incluido en el paquete.


## Aplicaciones fuera de línea
{: #offline_applications}

Para eliminar la necesidad de acceder a https://registry.npmjs.org, puede incluir todos los módulos de nodo que necesita su aplicación dentro de la aplicación.  Para ello, ejecute `npm install`para todos los módulos que necesite su aplicación e incluya el directorio *node_modules* resultante con la aplicación enviada por push.

Las dependencias pueden tener dependencias, que tienen dependencias y así sucesivamente, pero el `package.json` sólo contiene las dependencias de nivel superior. Si una de las dependencias utiliza un rango del package.json y se lanza una nueva versión del mismo, los módulos del directorio node_modules pueden quedarse obsoletos. *Shrinkwrap* le ayuda a bloquear todas las versiones de dependencias para que esto no ocurra.  Para utilizar shrinkwrap, empiece con un directorio vacío o limpio de `node_modules`. A continuación, en el directorio raíz del proyecto, ejecute:


1. `npm install`
1. `npm dedupe`
2. `npm shrinkwrap`

Esto puede cambiar el `package.json` y añadir `npm-shrinkwrap.json` en el directorio raíz.
Siempre que realice un cambio en las dependencias del archivo `package.json`, repita los pasos el `npm dedupe` y `shringwrap`.

## Cómo trabajar con un proxy
{: #working_with_proxy}

En algunos entornos como [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) y [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), se puede configurar un proxy. Consulte [Cómo trabajar con un proxy](/docs/manageapps/workingWithProxy.html) para obtener más detalles.
