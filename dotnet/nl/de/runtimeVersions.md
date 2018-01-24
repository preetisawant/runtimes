---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Laufzeitversionen
{: #runtime_vertsions}


{: shortdesc}

## Unterstützte Versionen
{: #supported_versions}
Dieses Buildpack unterstützt die folgenden Versionen. Versionen, die als veraltet markiert sind, werden in einem künftigen Release des Buildpacks entfernt.  Siehe [Microsoft Support Statement für LTS- und Current-Releases](https://www.microsoft.com/net/core/support).

### project.json-Tools (nicht mehr verwendet)

| .NET SDK-Version        | Standard |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   Nein    |

### MSBuild SDK-Tools

| .NET SDK-Version        | Standard |
|-------------------------|---------|
| 1.0.3                   |   Nein    |
| 1.0.4                   |   Ja   |
| 1.1.0-preview1-005051   |   Nein    |
| 2.0.0-preview1-005977   |   Nein    |
| 2.0.0-preview2-006497   |   Nein    |

### .NET Core-Laufzeitversionen

| .NET Core-Laufzeitversion | Releasetyp  | Standard |
|---------------------------|---------------|---------|
| 1.0.3 (nicht mehr verwendet)        | LTS           |   Nein    |
| 1.0.4 (nicht mehr verwendet)        | LTS           |   Nein    |
| 1.0.5                     | LTS           |   Ja   |
| 1.1.0 (nicht mehr verwendet)        | Current       |   Nein    |
| 1.1.1 (nicht mehr verwendet)        | Current       |   Nein    |
| 1.1.2                     | Current       |   Nein    |
| 2.0.0-preview1-002111-00  | LTS (preview) |   Nein    |
| 2.0.0-preview2-25407-01   | LTS (preview) |   Nein    |

## .NET SDK-Version angeben

Steuern Sie die .NET SDK-Version mit der optionalen Datei 'global.json' im Stammverzeichnis der Anwendung. Beispiel:
```
   {
      "sdk": {
        "version": "2.0.0-preview2-006497"
      }
   }
```
{: codeblock}

Falls nicht anders angegeben, wird das MSBuild-Tool für die letzte LTS-GA-Laufzeit (LTS, Long-term-support) verwendet.  Um das Tool 'project.json' zu verwenden, können Sie eine der oben aufgelisteten Versionen von 'project.json' angeben. Sie sollten dabei jedoch beachten, dass diese Versionen in Zukunft entfernt werden.
