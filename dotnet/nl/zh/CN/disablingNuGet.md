---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 禁用 NuGet 数据包高速缓存
{: #disabling_the_nuget_package_cache}

在某些情况下，可能有必要清除应用程序的 NuGet 数据包高速缓存。这将清除所有现有高速缓存的 NuGet 数据包，并阻止 buildpack 对任何新的数据包进行高速缓存。

要清除高速缓存，可以通过使用 {{site.data.keyword.Bluemix_notm}} CLI 将 `CACHE_NUGET_PACKAGES` 环境变量设置为 `false`：

```shell
  ibmcloud cf set-env <app_name> CACHE_NUGET_PACKAGES false
```
{: codeblock}

或者，可以在应用程序的 `manifest.yml` 文件中将 `CACHE_NUGET_PACKAGES` 环境变量设置为 `false`：

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
{: codeblock}
