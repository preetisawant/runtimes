---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Désactiver le cache de packages NuGet
{: #disabling_the_nuget_package_cache}

Dans certains cas, il est nécessaire d'effacer le cache de packages NuGet de votre application.  Cela aura pour effet d'effacer du cache tous les packages NuGet existants, mais aussi d'empêcher le pack de construction d'en mémoriser d'autres.

A cet effet, vous pouvez mettre à `false` la variable d'environnement `CACHE_NUGET_PACKAGES` en utilisant le client de ligne de commande pour {{site.data.keyword.Bluemix_notm}} :

```shell
  ibmcloud cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

Vous pouvez aussi mettre à `false` la variable d'environnement `CACHE_NUGET_PACKAGES` dans le fichier manifest.yml de votre application :

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
