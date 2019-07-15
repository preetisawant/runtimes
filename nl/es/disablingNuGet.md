---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Inhabilitar la memoria caché del paquete NuGet
{: #disabling_the_nuget_package_cache}

En algunas situaciones puede ser necesario borrar la memoria caché del paquete NuGet para la aplicación.  Esto borrará los paquetes NuGet existentes en memoria caché e impedirá que el paquete de compilación almacene en memoria caché paquetes nuevos.

Puede hacerlo estableciendo la variable de entorno `CACHE_NUGET_PACKAGES` en `false` con la CLI de {{site.data.keyword.Bluemix_notm}}:

```shell
  ibmcloud cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

Como alternativa, puede establecer la variable de entorno `CACHE_NUGET_PACKAGES` en `false` en el archivo manifest.yml de la aplicación:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
