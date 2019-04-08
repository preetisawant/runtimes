---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
subcollection: "Nodejs"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Versiones disponibles
{: #available_versions}

{{site.data.keyword.Bluemix}} proporciona todos [los modos de ejecución de Node.js disponibles actualmente](http://nodejs.org/dist/). De los tiempos de ejecución disponibles, {{site.data.keyword.IBM_notm}} proporciona versiones específicas que contienen mejoras y correcciones de errores. Consulte [Últimas actualizaciones del paquete de compilación Node.js](/docs/runtimes/nodejs/updates.html) para obtener más información sobre las versiones soportadas.
{: shortdesc}

El paquete de compilación Node.js almacena en caché las versiones de tiempo de ejecución de {{site.data.keyword.IBM_notm}}. Si utiliza {{site.data.keyword.IBM_notm}} SDK para el tiempo de ejecución de Node.js en la aplicación, el rendimiento de la aplicación es más rápido cuando la envía por push a {{site.data.keyword.Bluemix_notm}}.

## Especificación de una versión

* Utilice el parámetro **nodo** en la sección **motores** del archivo **package.json** para especificar la versión de tiempo de ejecución de Node.js que desee ejecutar.

* Si necesita especificar una versión de `npm` que no sea la versión empaquetada con Node.js, utilice el parámetro `npm` en la sección `engines` del archivo `package.json`.  

Consulte el siguiente ejemplo:

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}

**Nota:** especifique siempre una versión de nodo en el archivo `package.json`. Si no se especifica una versión, se utiliza la última versión del nodo.
