---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Desativar o cache de pacotes NuGet
{: #disabling_the_nuget_package_cache}

Em algumas situações, pode ser necessário limpar o cache de pacotes NuGet para o aplicativo.  Isso limpa qualquer pacotes NuGet existente armazenado em cache e impede que o buildpack armazene em cache qualquer novo pacote.

É possível limpar o cache definindo a variável de ambiente `CACHE_NUGET_PACKAGES` como `false` usando a CLI do {{site.data.keyword.Bluemix_notm}}:

```shell
  ibmcloud cf set-env < app_name> CACHE_NUGET_PACKAGES false
```
{: codeblock}

Como alternativa, é possível configurar a variável de ambiente `CACHE_NUGET_PACKAGES` como `false` no arquivo `manifest.yml` do aplicativo:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
{: codeblock}
