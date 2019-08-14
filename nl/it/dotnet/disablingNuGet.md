---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Disabilita la cache dei pacchetti NuGet
{: #disabling_the_nuget_package_cache}

In alcune situazioni, potrebbe essere necessario cancellare la cache dei pacchetti NuGet per la tua applicazione.  In questo modo cancelli tutti i pacchetti NuGet memorizzati nella cache esistenti ed eviti che il pacchetto di build memorizzi nella cache eventuali nuovi pacchetti.

Puoi cancellare la cache impostando la variabile di ambiente `CACHE_NUGET_PACKAGES` su `false` utilizzando la CLI {{site.data.keyword.Bluemix_notm}}:

```shell
  ibmcloud cf set-env <app_name> CACHE_NUGET_PACKAGES false
```
{: codeblock}

In alternativa, puoi impostare la variabile di ambiente `CACHE_NUGET_PACKAGES` su `false` nel file `manifest.yml` della tua applicazione:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
{: codeblock}
