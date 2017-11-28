---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versions d'environnement d'exécution
{: #runtime_vertsions}


{: shortdesc}

## Versions prises en charge
{: #supported_versions}
Ce pack de construction prend en charge les versions suivantes (les versions indiquées comme obsolètes seront supprimées dans une édition ultérieure du pack de construction). Consultez la [déclaration Microsoft de support pour les éditions LTS (Long Term Support) et les éditions actuelles](https://www.microsoft.com/net/core/support) (document en anglais).

### Outils project.json (déprécié)

| Version de .NET SDK     | Par défaut |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   Non   |

### Outils MSBuild SDK

| Version de .NET SDK     | Par défaut|
|-------------------------|---------|
| 1.0.3                   |   Non      |
| 1.0.4                   |   Oui      |
| 1.1.0-preview1-005051   |   Non      |
| 2.0.0-preview1-005977   |   Non      |
| 2.0.0-preview2-006497   |   Non      |

### Versions de l'environnement d'exécution .NET Core

| Version de l'env. d'exécution .NET Core | Type d'édition  | Par défaut |
|---------------------------|---------------|---------|
| 1.0.3 (obsolète)                 | LTS             |   Non      |
| 1.0.4 (obsolète)                 | LTS             |   Non      |
| 1.0.5                            | LTS             |   Oui      |
| 1.1.0 (obsolète)                 | Actuel          |   Non      |
| 1.1.1 (obsolète)                 | Actuel          |   Non      |
| 1.1.2                            | Actuel          |   Non      |
| 2.0.0-preview1-002111-00         | LTS (preview)   |   Non      |
| 2.0.0-preview2-25407-01          | LTS (preview)   |   Non      |

## Spécification de la version de .NET SDK

Contrôlez la version de .NET SDK avec un fichier global.json optionnel placé dans le répertoire racine de l'application. Par exemple :
```
   {
      "sdk": {
        "version": "2.0.0-preview2-006497"
      }
   }
```
{: codeblock}

En l'absence d'indication, les outils MSBuild du contexte d'exécution LTS (Long-Term-Support) GA le plus récent sont utilisés. Pour utiliser les outils project.json, vous pouvez spécifier l'une des versions de project.json listées plus haut, mais gardez à l'esprit que ces versions sont amenées à disparaître dans le futur.
