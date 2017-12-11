---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-31"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


#アプリケーションのコンパイル、パブリッシュ、およびデプロイ
{: #publish_configure_deploy}

## Release 構成でのアプリケーションのコンパイル (MSBuild の場合のみ)
{: #compiling_in_release_configuration}

MSBuild ベースのプロジェクトは、ステージング時に `dotnet publish` コマンドを使用してパブリッシュされるようになっています。デフォルトでは、ビルドパックは、`Debug` 構成でアプリケーションをパブリッシュします。
`Release` 構成でアプリケーションをパブリッシュするには、`PUBLISH_RELEASE_CONFIG` 環境変数を `true` に設定します。

これを行うには、CloudFoundry CLI で以下のコマンドを使用します。

```shell
  cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

あるいは、アプリケーションの manifest.yml ファイルに以下のように変数を設定することもできます。

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## パブリッシュされたアプリケーションのプッシュ
{: #pushing_published_app}

ビルドパックが外部のバイナリーをダウンロードしないように、アプリケーションに必要なバイナリーをすべて組み込む場合、パブリッシュされた*自己完結型*アプリケーションをプッシュすることができます。自己完結型アプリケーションについて詳しくは、[『.NET Core App Types』](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}を参照してください。

アプリケーションをパブリッシュするには、次のようなコマンドを発行します。
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

自己完結型アプリケーションの場合、次に、以下のディレクトリーからアプリケーションをプッシュできます。
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}

ポータブル・アプリケーションの場合、以下のディレクトリーからアプリケーションをプッシュできます。
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}

また、アプリケーションで manifest.yml ファイルを使用している場合は、manifest.yml でパブリッシュ出力フォルダーへのパスを指定できます。これにより、アプリケーションをプッシュする際に、そのフォルダーに入る必要がなくなります。

## 複数のプロジェクトを含むアプリケーションのデプロイ
{: #developing_apps_with_multiple_projects}

複数のプロジェクトを含むアプリケーションをデプロイする場合、どのプロジェクトをビルドパックでメイン・プロジェクトとして実行するかを指定する必要があります。これを行うには、ソリューションのルート・フォルダー内に、メイン・プロジェクトへのパスを設定する .deployment ファイルを作成します。メイン・プロジェクトへのパスは、プロジェクト・フォルダーまたはプロジェクト・ファイル (.xproj または .csproj) として指定できます。

例えば、あるソリューションの *src* フォルダー内に 3 つのプロジェクト *MyApp.DAL*、*MyApp.Services*、および *MyApp.Web* が含まれており、*MyApp.Web* がメイン・プロジェクトである場合、.deployment ファイルのフォーマットは、次のようになります。
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

この例では、*MyApp.DAL* プロジェクトと *MyApp.Services* プロジェクトが *MyApp.Web* の project.json ファイルに依存関係としてリストされている場合、ビルドパックはこれらのプロジェクトを自動的にコンパイルします。しかし、dotnet run -p src/MyApp.Web コマンドを使用した場合は、ビルドパックはメイン・プロジェクトである *MyApp.Web* の実行のみを試みます。
