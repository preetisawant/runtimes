---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versioni di runtime
{: #runtime_vertsions}


{: shortdesc}

## Versioni supportate
{: #supported_versions}
Questo pacchetto di build supporta le seguenti versioni, quelle contrassegnate come obsolete saranno rimosse in una futura release del pacchetto di build.  Consulta [Microsoft's support statement for LTS and Current releases](https://www.microsoft.com/net/core/support).

### Strumento project.json (obsoleto)

| Versione SDK .NET        | Predefinito |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   No    |

### Strumento SDK MSBuild

| Versione SDK .NET        | Predefinito |
|-------------------------|---------|
| 1.0.3                   |   No    |
| 1.0.4                   |   Sì   |
| 1.1.0-preview1-005051   |   No    |
| 2.0.0-preview1-005977   |   No    |
| 2.0.0-preview2-006497   |   No    |

### Versioni runtime .NET Core

| Version runtime .NET Core | Tipo di rilascio  | Predefinito |
|---------------------------|---------------|---------|
| 1.0.3 (obsoleta)        | LTS           |   No    |
| 1.0.4 (obsoleta)        | LTS           |   No    |
| 1.0.5                     | LTS           |   Sì   |
| 1.1.0 (obsoleta)        | Corrente       |   No    |
| 1.1.1 (obsoleta)        | Corrente       |   No    |
| 1.1.2                     | Corrente       |   No    |
| 2.0.0-preview1-002111-00  | LTS (anteprima) |   No    |
| 2.0.0-preview2-25407-01   | LTS (anteprima) |   No    |

## Specifica della versione della SDK .NET

Controlla la versione della SDK .NET con un global.json facoltativo nella directory root dell'applicazione. Ad esempio:
```
   {
      "sdk": {
        "version": "2.0.0-preview2-006497"
      }
   }
```
{: codeblock}

Se non specificato, viene utilizzato lo strumento MSBuild per l'ultimo runtime GA Long-term-support (LTS). Per utilizzare lo strumento project.json, puoi specificare una delle versioni project.json precedentemente elencate ma devi anche tenere presente che queste versioni saranno rimosse in futuro.
