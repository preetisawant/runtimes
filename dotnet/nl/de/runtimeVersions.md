---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Laufzeitversionen
{: #runtime_versions}


{: shortdesc}

## Unterstützte Versionen
{: #supported_versions}

Dieses Buildpack unterstützt die folgenden Versionen. Versionen, die als veraltet markiert sind, werden in einem künftigen Release des Buildpacks entfernt.  Siehe [Microsoft Support Statement für LTS- und Current-Releases](https://www.microsoft.com/net/core/support).

### project.json-Tools (veraltet)

| .NET SDK-Version        | Standard |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   Nein    |

### MSBuild SDK-Tools

| .NET SDK-Version        | Standard          |
|-------------------------|------------------|
| 1.0.4                   |   Nein             |
| 1.1.0                   |   Ja (nur F#)  |
| 2.0.0                   |   Ja            |

### .NET Core-Laufzeitversionen

| .NET Core-Laufzeitversion | Releasetyp      |
|---------------------------|-------------------|
| 1.0.4 (veraltet)        | LTS               |
| 1.0.5                     | LTS               |
| 1.1.1 (veraltet)        | LTS               |
| 1.1.2                     | LTS               |
| 2.0.0-preview2-25407-01   | Current (Vorschau) |
| 2.0.0                     | Current           |

## .NET SDK-Version angeben

Steuern Sie die .NET SDK-Version mit der optionalen Datei `global.json` im Stammverzeichnis der Anwendung. Beispiel:
```
   {
      "sdk": {
        "version": "2.0.0"
      }
   }
```
{: codeblock}

Wenn nicht angegeben, werden die aktuellsten MSBuild-Tools verwendet.  Wenn Sie die 'project.json'-Tools verwenden wollen, können Sie eine der aufgeführten Versionen von 'project.json' angeben. Beachten Sie dabei jedoch, dass diese Versionen in Zukunft entfernt werden.  Wenn die angegebene Version im Buildpack nicht enthalten ist, wird die Standardversion verwendet. In diesem Fall wird eine Warnung in den Staging-Protokollen aufgezeichnet.
