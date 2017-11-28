---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 停用 NuGet 套件快取
{: #disabling_the_nuget_package_cache}

在某些情況下，可能需要清除應用程式的 NuGet 套件快取。這麼做將會清除任何現有的已快取 NuGet 套件，並防止建置套件快取任何新的套件。

這項作業的作法是使用 CloudFoundry CLI，將 `CACHE_NUGET_PACKAGES` 環境變數設為 `false`：

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

或者，您也可以在應用程式的 manifest.yml 檔案中將 `CACHE_NUGET_PACKAGES` 環境變數設為 `false`：

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
