---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# NuGet-Paketcache inaktivieren
{: #disabling_the_nuget_package_cache}

In einigen Situationen ist es möglicherweise erforderlich, den NuGet-Paketcache für Ihre Anwendung zu bereinigen.  Bei diesem Vorgang werden alle vorhandenen NuGet-Pakete, die im Cache gespeichert sind, bereinigt und es wird verhindert, dass das Buildpack neue Pakete im Cache speichert.

Sie können dies erreichen, indem Sie die Umgebungsvariable `CACHE_NUGET_PACKAGES` über die {{site.data.keyword.Bluemix_notm}}-CLI auf den Wert `false` setzen:

```shell
  ibmcloud cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

Alternativ können Sie die Umgebungsvariable `CACHE_NUGET_PACKAGES` in der Datei 'manifest.yml' Ihrer Anwendung auf den Wert `false` setzen:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
