---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versions d'environnement d'exécution
{: #runtime_versions}


{: shortdesc}

## Versions prises en charge
{: #supported_versions}

Ce pack de construction prend en charge les versions suivantes (les versions indiquées comme obsolètes seront supprimées dans une édition ultérieure du pack de construction).  Consultez la [déclaration Microsoft de support pour les éditions LTS (Long Term Support) et les éditions actuelles](https://www.microsoft.com/net/core/support) (document en anglais).

### Outils project.json (déprécié)

| Version de .NET SDK        | Par défaut |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   Non    |

### Outils MSBuild SDK

| Version de .NET SDK        | Par défaut          |
|-------------------------|------------------|
| 1.0.4                   |   Non             |
| 1.1.0                   |   Oui (F# slmt)  |
| 2.0.0                   |   Oui            |

### Versions de l'environnement d'exécution .NET Core

| Version de l'env. d'exécution .NET Core | Type d'édition      |
|---------------------------|-------------------|
| 1.0.4 (obsolète)        | LTS               |
| 1.0.5                     | LTS               |
| 1.1.1 (obsolète)        | LTS               |
| 1.1.2                     | LTS               |
| 2.0.0-preview2-25407-01   | En cours (aperçu) |
| 2.0.0                     | Actuel           |

## Spécification de la version de .NET SDK

Contrôlez la version de .NET SDK avec un fichier `global.json` optionnel placé dans le répertoire racine de l'application. Par exemple :
```
   {
      "sdk": {
        "version": "2.0.0"
      }
   }
```
{: codeblock}

Si non spécifié, les derniers outils MSBuild sont utilisés.  Pour utiliser les outils project.json, vous pouvez spécifier l'une des versions de project.json répertoriées, mais gardez à l'esprit que ces versions sont amenées à disparaître dans le futur.  Si la version spécifiée ne figure pas dans le pack de construction, la version par défaut est utilisée et un avertissement figure dans les journaux de préproduction.
