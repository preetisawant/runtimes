---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Desativar o cache de pacotes NuGet
{: #disabling_the_nuget_package_cache}

Em algumas situações, pode ser necessário limpar o cache de pacotes NuGet de seu aplicativo.  Fazer isso limpará quaisquer pacotes NuGet em cache existentes e evitará que o buildpack armazene em cache quaisquer novos pacotes.

Isso pode ser feito configurando a variável de ambiente `CACHE_NUGET_PACKAGES` como `false` usando o CloudFoundry CLI:

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

Como alternativa, é possível configurar a variável de ambiente `CACHE_NUGET_PACKAGES` como `false` no arquivo manifest.yml do aplicativo:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
