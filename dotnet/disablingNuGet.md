---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Disable the NuGet Package Cache
{: #disabling_the_nuget_package_cache}

In some situations it may be necessary to clear the NuGet package cache for your application.  Doing so will clear any existing cached NuGet packages and prevent the buildpack from caching any new packages.

You can do this by setting the `CACHE_NUGET_PACKAGES` environment variable to `false` using the {{site.data.keyword.Bluemix_notm}} CLI:

```shell
  ibmcloud cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

Alternatively, you can set the `CACHE_NUGET_PACKAGES` environment variable to `false` in your application's manifest.yml file:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
