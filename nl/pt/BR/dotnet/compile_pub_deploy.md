---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


#Compilar, publicar e implementar aplicativos
{: #publish_configure_deploy}

## Compilando seu aplicativo na configuração de liberação (apenas MSBuild)
{: #compiling_in_release_configuration}

Os projetos baseados em MSBuild são agora publicados usando o comando `dotnet publish` durante a preparação.  Por padrão, o buildpack publicará seu aplicativo na configuração de `Depuração`.
Para publicar seu aplicativo na configuração de `Liberação`, configure a variável de ambiente `PUBLISH_RELEASE_CONFIG` como `true`.

É possível fazer isso com a CLI do {{site.data.keyword.Bluemix_notm}} com o comando a seguir:

```shell
  ibmcloud cf set-env < app_name> PUBLISH_RELEASE_CONFIG true
```

Como alternativa, é possível configurar a variável no arquivo manifest.yml do aplicativo:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## Enviando por push um aplicativo publicado
{: #pushing_published_app}

Se você quiser que seu aplicativo contenha todos os binários necessários para que o buildpack não faça download de
qualquer binário externo, será possível enviar por push um aplicativo *autocontido* publicado.  Consulte
[Tipos de
app .NET Core](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window} para obter mais informações sobre
aplicativos autocontidos.

Para publicar um aplicativo, emita um comando como:
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

Para aplicativos autocontidos, o app poderá então ser enviado por push do diretório
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
específico.

Para aplicativos móveis, o app poderá ser enviado por push do diretório
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
específico.

Observe também que se você estiver usando um arquivo manifest.yml em seu
aplicativo, será possível especificar o caminho para a pasta de saída de publicação no
manifest.yml.  Assim, não é necessário estar nessa pasta quando enviar o aplicativo por
push.

## Implementando apps com diversos projetos
{: #developing_apps_with_multiple_projects}

Para implementar um app que contém diversos projetos, você precisará especificar
qual projeto deseja que o buildpack execute como projeto principal. Isso pode ser feito
criando um arquivo .deployment na pasta raiz da solução que configura o caminho para
o projeto principal. O caminho para o projeto principal pode ser especificado como a
pasta ou o arquivo do projeto (.xproj ou .csproj).

Por exemplo, se uma solução contendo três projetos,
*MyApp.DAL*, *MyApp.Services* e *MyApp.Web* na
pasta *src*, e *MyApp.Web* for o projeto principal, o formato
do arquivo .deployment será este:
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

Neste exemplo, o buildpack compilaria automaticamente os projetos
*MyApp.DAL* e *MyApp.Services* se eles estivessem listados como
dependências no arquivo project.json para *MyApp.Web*, mas o buildpack
somente tentaria executar o projeto principal, *MyApp.Web*, com dotnet run
-p src/MyApp.Web.
