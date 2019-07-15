---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}

El tiempo de ejecución de Go en {{site.data.keyword.Bluemix}} está basado en go_buildpack.
go_buildpack proporciona un entorno de ejecución completo para apps Go.
{: shortdesc}

go_buildpack se utiliza si la aplicación contiene un archivo denominado *.go.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} proporciona una aplicación de inicio de Go.  La aplicación de inicio Go es una sencilla app Go que ofrece una plantilla que puede utilizar para su app. Puede experimentar con la app de inicio y realizar y enviar cambios push al entorno de {{site.data.keyword.Bluemix_notm}}. Consulte [Utilización de las aplicaciones de iniciador](../common/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de iniciador.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de Go que utilizará la app estableciendo la propiedad GoVersion en el archivo Godeps/Godeps.json en la raíz de la aplicación. Por ejemplo:

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.8.3",
	"Deps": []
}
```
{: codeblock}
Para obtener más información, consulte [godep](https://github.com/tools/godep){: new_window}.

Cuando no se especifique una versión, se elegirá la versión 1.8.7 de forma predeterminada.

### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de Go están disponibles en el
[paquete de compilación de Go](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.8.20){: new_window}
instalado actualmente en {{site.data.keyword.Bluemix_notm}}:

* 1.6.3
* 1.6.4
* 1.7.5
* 1.7.6
* 1.8.6
* 1.8.7
* 1.9.3
* 1.9.4
* 1.10

Si la app requiere una versión de Go que no aparece en la lista,
puede utilizar el
[paquete de compilación de Go](https://github.com/cloudfoundry/go-buildpack.git){: new_window} externo para
desplegar la aplicación.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}

* [GoLang](http://golang.org/){: new_window}
* [Paquete de compilación de Cloud Foundry para Go](https://github.com/cloudfoundry/go-buildpack){: new_window}
