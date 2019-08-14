---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# NuGet パッケージのキャッシュの無効化
{: #disabling_the_nuget_package_cache}

場合によっては、アプリケーション用の NuGet パッケージのキャッシュをクリアする必要が生じることがあります。  そうすることにより、キャッシュに入れられている既存の NuGet パッケージは消去され、ビルドパックが新規パッケージをキャッシュに入れるのが防止されます。

以下のように {{site.data.keyword.Bluemix_notm}} CLI で `CACHE_NUGET_PACKAGES` 環境変数を `false` に設定することによって、キャッシュをクリアすることができます。

```shell
  ibmcloud cf set-env <app_name> CACHE_NUGET_PACKAGES false
```
{: codeblock}

あるいは、以下のようにアプリケーションの `manifest.yml` ファイルで `CACHE_NUGET_PACKAGES` 環境変数を `false` に設定することもできます。

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
{: codeblock}
