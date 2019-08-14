---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Désactiver le cache de packages NuGet
{: #disabling_the_nuget_package_cache}

Dans certains cas de figure, il peut s'avérer nécessaire d'effacer le cache de packages NuGet de votre application.  Cela a pour effet d'effacer du cache tous les packages NuGet existants, mais aussi d'empêcher le pack de construction d'en mémoriser d'autres.

Vous pouvez effacer le cache en définissant sur `false` la variable d'environnement `CACHE_NUGET_PACKAGES` à l'aide du client de ligne de commande pour {{site.data.keyword.Bluemix_notm}} :

```shell
  ibmcloud cf set-env <app_name> CACHE_NUGET_PACKAGES false
```
{: codeblock}

Vous pouvez aussi mettre à `false` la variable d'environnement `CACHE_NUGET_PACKAGES` dans le fichier `manifest.yml` de votre application :

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
{: codeblock}
