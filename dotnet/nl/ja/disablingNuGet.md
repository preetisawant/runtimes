---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# NuGet パッケージのキャッシュの無効化
{: #disabling_the_nuget_package_cache}

場合によっては、アプリケーションの NuGet パッケージのキャッシュをクリアする必要が生じることがあります。そうすることにより、キャッシュに入れられている既存の NuGet パッケージがクリアされ、ビルドパックで新規パッケージがキャッシュに入れられなくなります。

これを行うには、CloudFoundry CLI を使用して以下のように `CACHE_NUGET_PACKAGES` 環境変数を `false` に設定します。

```shell
  cf set-env <app_name> CACHE_NUGET_PACKAGES false
```

あるいは、アプリケーションの manifest.yml ファイルで、以下のように `CACHE_NUGET_PACKAGES` 環境変数を `false` に設定することもできます。

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
