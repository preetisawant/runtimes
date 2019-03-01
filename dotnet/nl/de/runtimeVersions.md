---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Laufzeitversionen
{: #runtime_versions}

## Unterstützte Versionen
{: #supported_versions}

Dieses Buildpack unterstützt die folgenden Versionen. Versionen, die als veraltet markiert sind, werden in einem künftigen Release des Buildpacks entfernt.  Siehe [Microsoft Support Statement für LTS- und Current-Releases](https://www.microsoft.com/net/core/support).


### .NET SDK-Version

| .NET SDK-Version        | Standard          |
|-------------------------|------------------|
| 2.1.403                 |   Ja            |
| 2.1.302                 |   Nein             |
| 2.0.3                   |   Nein             |
| 1.1.11                  |   Nein             |
| 1.1.10                  |   Nein             |
| 1.0.4                   |   Nein             |


### .NET Core-Laufzeitversionen

| .NET Core-Laufzeitversion | Releasetyp      |
|---------------------------|-------------------|
| 2.1.5                     | Current           |  
| 2.1.4                     | LTS               |
| 2.1.2                     | LTS               |
| 2.0.9                     | LTS               |
| 2.0.7                     | LTS               |
| 1.1.10                    | LTS               |
| 1.1.9                     | LTS               |
| 1.0.12                    | LTS               |
| 1.0.11                    | LTS               |


### .NET aspnetcore-Versionen

| .NET aspnetcore-Version | Releasetyp      |
|---------------------------|-------------------|
| 2.1.5                     | Current           |  
| 2.1.4                     | LTS               |
| 2.1.2                     | LTS               |



## .NET SDK-Version angeben

Steuern Sie die .NET SDK-Version mit der optionalen Datei `global.json` im Stammverzeichnis der Anwendung. Beispiel:
```
   {
      "sdk": {
        "version": "2.1.301"
      }
   }
```
{: codeblock}

Wenn nicht angegeben, werden die aktuellsten MSBuild-Tools verwendet.  Wenn Sie die 'project.json'-Tools verwenden wollen, können Sie eine der aufgeführten Versionen von 'project.json' angeben. Beachten Sie dabei jedoch, dass diese Versionen in Zukunft entfernt werden.  Wenn die angegebene Version im Buildpack nicht enthalten ist, wird die Standardversion verwendet. In diesem Fall wird eine Warnung in den Staging-Protokollen aufgezeichnet.
