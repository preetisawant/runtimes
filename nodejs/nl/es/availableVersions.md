---

copyright:
  years: 2015, 2017
lastupdated: "2017-06-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Versiones disponibles
{: #available_versions}

{{site.data.keyword.Bluemix}} proporciona todos [los modos de ejecución de Node.js disponibles actualmente](http://nodejs.org/dist/). De los modos de ejecución disponibles, IBM proporciona versiones específicas que contienen mejoras y arreglos de errores. Consulte [Últimas actualizaciones del paquete de compilación Node.js](/docs/runtimes/nodejs/updates.html) para obtener más información sobre las versiones soportadas.
{: shortdesc}

El paquete de compilación Node.js de IBM almacena en caché las versiones de tiempo de ejecución de IBM. Si utiliza IBM SDK para el tiempo de ejecución Node.js en la aplicación, el rendimiento de la aplicación es más rápido cuando la envía por push a Bluemix.

## Especificación de una versión

* Utilice el parámetro **nodo** en la sección **motores** del archivo **package.json** para especificar la versión de tiempo de ejecución de Node.js que desee ejecutar.

* Si necesita especificar una versión de npm que no sea la versión empaquetada con Node.js., utilice el parámetro **npm** en la sección **engines** del archivo **package.json**.   

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

**Nota:** debería especificarse siempre una versión de nodo en el archivo **package.json**. Si no, se utilizará la versión del nodo más reciente.
