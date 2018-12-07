---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versioni di runtime
{: #runtime_versions}

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
| 2.1.301                 |   Sì            |
| 2.1.300                 |   No             |
| 2.1.201                 |   No             |
| 2.0.3                   |   No             |
| 2.0.2                   |   No             |
| 1.1.9                   |   No             |
| 1.0.4                   |   No             |


### Versioni runtime .NET Core

| Version runtime .NET Core | Tipo di rilascio      |
|---------------------------|-------------------|
| 2.1.1                     | LTS               |
| 2.1.0                     | LTS               |
| 2.0.7                     | LTS               |
| 2.0.3                     | Corrente           |
| 2.0.2                     | Corrente           |
| 2.0.0                     | LTS               |
| 1.1.8                     | LTS               |
| 1.1.2                     | LTS               |
| 1.0.11                    | LTS               |
| 1.0.5                     | LTS               |
| 1.0.4                     | LTS               |

## Specifica della versione della SDK .NET

Controlla la versione della SDK .NET con un `global.json` facoltativo nella directory root dell'applicazione. Ad esempio:
```
   {
      "sdk": {
        "version": "2.1.301"
      }
   }
```
{: codeblock}

Se non viene specificato, vengono utilizzati gli strumenti MSBuild più recenti.  Per utilizzare gli strumenti project.json, puoi specificare una delle versioni project.json elencate ma tieni presente che queste versioni saranno rimosse in futuro.  Se la versione specificata non è inclusa nel pacchetto di build, viene utilizzata la versione predefinita e viene visualizzata un'avvertenza nei log di preparazione.
