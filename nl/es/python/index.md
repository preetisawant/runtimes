---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-05"
subcollection: "Python"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}

El tiempo de ejecución de Python en {{site.data.keyword.Bluemix}} está basado en el python_buildpack.
El python_buildpack proporciona un entorno de ejecución completo para apps Python 2 y Python 3.
{: shortdesc}

El python_buildpack se utilizará si el directorio raíz de la app contiene un archivo requirements.txt o un archivo setup.py.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} proporciona una aplicación de inicio Python.  La aplicación de inicio Python es una sencilla app Python que ofrece una plantilla que puede utilizar para su app. Puede experimentar con la app de iniciador, y realizar y enviar por push cambios en el entorno de {{site.data.keyword.Bluemix_notm}}.  Consulte [Utilización de las aplicaciones de inicio](docs/runtimes-common/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de Python que va a utilizar la app estableciendo python-versionnumber en el archivo runtime.txt en la raíz de la aplicación. Por ejemplo:

```
python-3.6.4
```
{: codeblock}

Cuando no se especifique una versión, se elegirá la versión 2.7.14 de forma predeterminada.

### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de Python están disponibles en el
[paquete de compilación de Python](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.6.11)
actualmente instalado en {{site.data.keyword.Bluemix_notm}}:

* 2.7.13
* 2.7.14
* 3.3.6
* 3.3.7
* 3.4.7
* 3.4.8
* 3.5.4
* 3.5.5
* 3.6.3
* 3.6.4

Si la aplicación requiere una versión de Python que no aparece en la lista,
puede utilizar el
[paquete de compilación de Python](https://github.com/cloudfoundry/python-buildpack) externo para
desplegar la app.
