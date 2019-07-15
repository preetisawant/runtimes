---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


#Compiler, publier et déployer des applications
{: #publish_configure_deploy}

## Compilation de votre application en configuration Release (MSBuild uniquement)
{: #compiling_in_release_configuration}

Les projets basés sur MSBuild sont à présent publiés en utilisant la commande `dotnet publish` durant le passage en préproduction (staging).  Par défaut, le pack de construction publiera votre application en configuration `Debug`.
Pour qu'elle soit publiée en configuration `Release`, mettez à `true` la variable d'environnement `PUBLISH_RELEASE_CONFIG`.

Vous pouvez pour cela utiliser l'interface CLI {{site.data.keyword.Bluemix_notm}} avec la commande suivante :

```shell
  ibmcloud cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

Vous pouvez aussi définir la variable dans le fichier manifest.yml de votre application :

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## Envoi par commande push d'une application publiée
{: #pushing_published_app}

Si votre application doit contenir tous ses fichiers binaires requis et éviter ainsi que le pack de construction ne télécharge des fichiers binaires externes, vous pouvez l'envoyer par commande push sous forme d'application *autonome* publiée.  Consultez [.NET Core App Types](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window} pour plus d'informations sur les applications autonomes.

Pour publier une application, exécutez une commande telle que la suivante :
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

Les applications autonomes peuvent ensuite être envoyées par commande push à partir de
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
.

Les applications portables peuvent être envoyées par commande push à partir de
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
.

En outre, si vous utilisez un fichier manifest.yml dans votre application, vous pouvez spécifier le chemin d'accès au dossier de sortie de la publication dans votre fichier manifest.yml.  Ensuite, il n'est pas nécessaire de se placer dans ce dossier lors de l'envoi par commande push de l'application.

## Déploiement d'applications comportant plusieurs projets
{: #developing_apps_with_multiple_projects}

Pour déployer une application qui contient plusieurs projets, vous devez spécifier le projet que le pack de construction doit exécuter comme projet principal. Pour ce faire, créez un fichier .deployment dans le dossier racine de la solution qui définit le chemin d'accès vers le projet principal. Le chemin d'accès au projet principal peut être spécifié comme dossier de projet ou comme fichier de projet (.xproj ou .csproj).

Par exemple, si une solution contient trois projets, *MyApp.DAL*, *MyApp.Services* et *MyApp.Web* dans le dossier *src*, et si *MyApp.Web* est le projet principal, le format du fichier .deployment doit être le suivant :
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

Dans cet exemple, le pack de construction compile automatiquement les projets *MyApp.DAL* et *MyApp.Services* s'ils sont répertoriés en tant que dépendances dans le fichier project.json pour *MyApp.Web*, mais le pack de construction tente uniquement d'exécuter le projet principal, *MyApp.Web*, avec dotnet run -p src/MyApp.Web.
