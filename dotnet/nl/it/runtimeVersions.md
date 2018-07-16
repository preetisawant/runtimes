---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versioni di runtime
{: #runtime_versions}


{: shortdesc}

## Versioni supportate
{: #supported_versions}

Questo pacchetto di build supporta le seguenti versioni, quelle contrassegnate come obsolete saranno rimosse in una futura release del pacchetto di build.  Consulta [Microsoft's support statement for LTS and Current releases](https://www.microsoft.com/net/core/support).

### Strumento project.json (obsoleto)

| Versione SDK .NET        | Predefinito |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   No    |

### Strumento SDK MSBuild

| Versione SDK .NET        | Predefinito          |
|-------------------------|------------------|
| 1.0.4                   |   No             |
| 1.1.0                   |   Sì (solo F#)  |
| 2.0.0                   |   Sì            |

### Versioni runtime .NET Core

| Version runtime .NET Core | Tipo di rilascio      |
|---------------------------|-------------------|
| 1.0.4 (obsoleta)        | LTS               |
| 1.0.5                     | LTS               |
| 1.1.1 (obsoleta)        | LTS               |
| 1.1.2                     | LTS               |
| 2.0.0-preview2-25407-01   | Corrente (anteprima) |
| 2.0.0                     |Corrente       |

## Specifica della versione della SDK .NET

Controlla la versione della SDK .NET con un `global.json` facoltativo nella directory root dell'applicazione. Ad esempio:
```
   {
      "sdk": {
        "version": "2.0.0"
      }
   }
```
{: codeblock}

Se non viene specificato, vengono utilizzati gli strumenti MSBuild più recenti. Per utilizzare gli strumenti project.json, puoi specificare una delle versioni project.json elencate ma tieni presente che queste versioni saranno rimosse in futuro. Se la versione specificata non è inclusa nel pacchetto di build, viene utilizzata la versione predefinita e viene visualizzata un'avvertenza nei log di preparazione.
