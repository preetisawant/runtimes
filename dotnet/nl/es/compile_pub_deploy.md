---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


#Compilar, publicar y desplegar aplicaciones
{: #publish_configure_deploy}

## Compilación de la aplicación en la configuración del Release (solo MSBuild)
{: #compiling_in_release_configuration}

Los proyectos que se basan en MSBuild ahora se publican utilizando el mandato `dotnet publish` durante la transferencia.  De forma predeterminada, el paquete de compilación publicará la aplicación en la configuración `Debug`.
Para publicar la aplicación en la configuración `Release`, establezca la variable de entorno `PUBLISH_RELEASE_CONFIG` en `true`.

Puede hacerlo con la CLI de {{site.data.keyword.Bluemix_notm}} con el siguiente mandato:

```shell
  ibmcloud cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

Como alternativa, puede establecer la variable en el archivo manifest.yml de la aplicación:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## Envío por push de una aplicación publicada
{: #pushing_published_app}

Si desea que la aplicación contenga todos sus binarios necesarios de modo que el paquete de compilación no descargue ningún binario externo, puede enviar por push una aplicación *autocontenida* publicada.  Consulte [Tipos de app de .NET Core ](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window} para obtener más información sobre aplicaciones autocontenidas.

Para publicar un problema de aplicación, emita un mandato como el siguiente:
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

Para aplicaciones autocontenidas, la app se podrá enviar por push desde el directorio
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
.

Para aplicaciones portables, la app se podrá enviar por push desde el directorio
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
.

Tenga en cuenta que si utiliza un archivo manifest.yml en la aplicación, puede especificar la vía de acceso a la carpeta de salida de publicación en manifest.yml.  Después no tendrá que estar en esa carpeta cuando envíe por push la aplicación.

## Despliegue de apps con varios proyectos
{: #developing_apps_with_multiple_projects}

Para desplegar una app que contiene varios proyectos, será necesario especificar qué proyecto desea que el paquete de compilación ejecute como proyecto principal. Esto puede llevarse a cabo creando un archivo .deployment en la carpeta raíz de la solución que establece la vía de acceso al proyecto principal. La vía de acceso al proyecto principal puede especificarse como carpeta de proyecto o el archivo de proyecto (.xproj o .csproj).

Por ejemplo, si una solución que contiene tres proyectos, *MyApp.DAL*, *MyApp.Services* y *MyApp.Web* en la carpeta *src*, y *MyApp.Web* es el proyecto principal, el formato del archivo .deployment sería el siguiente:
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

En este ejemplo, el paquete de compilación compila automáticamente los proyectos *MyApp.DAL* y *MyApp.Services* si están listados como dependencias en el archivo project.json para *MyApp.Web*, pero el paquete de compilación sólo intentará ejecutar el proyecto principal, *MyApp.Web*, con dotnet run -p src/MyApp.Web.
