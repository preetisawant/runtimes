---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versioni di runtime
{: #runtime_versions}

## Versioni supportate
{: #supported_versions}

Questo pacchetto di build supporta le seguenti versioni, quelle contrassegnate come obsolete saranno rimosse in una futura release del pacchetto di build.  Consulta [Microsoft's support statement for LTS and Current releases](https://www.microsoft.com/net/core/support).


### Versione SDK .NET

| Versione SDK .NET        | Predefinito          |
|-------------------------|------------------|
| 2.1.403                 |   Sì            |
| 2.1.302                 |   No             |
| 2.0.3                   |   No             |
| 1.1.11                  |   No             |
| 1.1.10                  |   No             |
| 1.0.4                   |   No             |


### Versioni runtime .NET Core

| Version runtime .NET Core | Tipo di rilascio      |
|---------------------------|-------------------|
| 2.1.5                     | Corrente           |  
| 2.1.4                     | LTS               |
| 2.1.2                     | LTS               |
| 2.0.9                     | LTS               |
| 2.0.7                     | LTS               |
| 1.1.10                    | LTS               |
| 1.1.9                     | LTS               |
| 1.0.12                    | LTS               |
| 1.0.11                    | LTS               |


### Versioni .NET aspnetcore

| Versione .NET aspnetcore | Tipo di rilascio      |
|---------------------------|-------------------|
| 2.1.5                     | Corrente           |  
| 2.1.4                     | LTS               |
| 2.1.2                     | LTS               |



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
