---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-20"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versions d'environnement d'exécution
{: #runtime_versions}

## Versions prises en charge
{: #supported_versions}

Ce pack de construction prend en charge les versions suivantes (les versions indiquées comme obsolètes seront supprimées dans une édition ultérieure du pack de construction).  Consultez la [déclaration Microsoft de support pour les éditions LTS (Long Term Support) et les éditions actuelles](https://www.microsoft.com/net/core/support) (document en anglais).


### Version de .NET SDK

| Version de .NET SDK        | Par défaut    |
|-------------------------|------------------|
| 2.2.104                 |   Oui            |
| 2.1.504                 |   Non            |
| 2.1.403                 |   Non            |
| 2.0.3                   |   Non            |
| 1.1.12                  |   Non            |
| 1.1.11                  |   Non            |
| 1.0.4                   |   Non            |


### Versions de l'environnement d'exécution .NET Core

| Version env. exécution .NET Core | Type d'édition      |
|---------------------------|-------------------|
| 2.2.2                     | Actuel           |  
| 2.2.1                     | LTS               |
| 2.1.8                     | LTS               |
| 2.1.7                     | LTS               |
| 2.0.9                     | LTS               |
| 2.0.7                     | LTS               |
| 1.1.11                    | LTS               |
| 1.1.10                    | LTS               |
| 1.0.12                    | LTS               |
| 1.0.11                    | LTS               |


### Version .NET aspnetcore

| Version .NET aspnetcore | Type d'édition        |
|---------------------------|-------------------|
| 2.2.2                     | Actuel           |  
| 2.2.1                     | LTS               |
| 2.1.8                     | LTS               |
| 2.1.7                     | LTS               |



## Spécification de la version de .NET SDK

Contrôlez la version de .NET SDK avec un fichier `global.json` optionnel placé dans le répertoire racine de l'application. Par exemple :
```
   {
      "sdk": {
        "version": "2.2.104"
      }
   }
```
{: codeblock}

Si non spécifié, les derniers outils MSBuild sont utilisés.  Pour utiliser les outils project.json, vous pouvez spécifier l'une des versions de project.json répertoriées, mais gardez à l'esprit que ces versions sont amenées à disparaître dans le futur.  Si la version spécifiée ne figure pas dans le pack de construction, la version par défaut est utilisée et un avertissement figure dans les journaux de préproduction.
