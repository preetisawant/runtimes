---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# NuGet-Paketcache inaktivieren
{: #disabling_the_nuget_package_cache}

In einigen Situationen ist es möglicherweise erforderlich, den NuGet-Paketcache für Ihre Anwendung zu bereinigen. Bei diesem Vorgang werden alle vorhandenen NuGet-Pakete, die im Cache gespeichert sind, bereinigt und es wird verhindert, dass das Buildpack neue Pakete im Cache speichert. 

Sie können dies durch die Angabe des Wertes `false` für die Umgebungsvariable `CACHE_NUGET_PACKAGES` erreichen. Dazu verwenden Sie die CloudFoundry-CLI:

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

Alternativ können Sie für die Umgebungsvariable `CACHE_NUGET_PACKAGES` in der Datei 'manifest.yml' Ihrer Anwendung den Wert `false` festlegen: 

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
