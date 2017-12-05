---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Disabilita la cache del pacchetto NuGet
{: #disabling_the_nuget_package_cache}

In alcune situazioni potrebbe essere necessario cancellare la cache del pacchetto NuGet della tua applicazione.  In questo modo cancelli tutti i pacchetti NuGet nella cache esistenti ed eviti la memorizzazione nella cache del pacchetto di build per tutti i nuovi pacchetti.

Puoi farlo impostando la variabile di ambiente `CACHE_NUGET_PACKAGES` su `false` utilizzando la CLI CloudFoundry:

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

In alternativa, puoi impostare la variabile di ambiente `CACHE_NUGET_PACKAGES` su `false` nel file manifest.yml della tua applicazione:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
