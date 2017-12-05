---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versiones de tiempo de ejecución
{: #runtime_vertsions}


{: shortdesc}

## Versiones soportadas
{: #supported_versions}
Este paquete de compilación da soporte a las versiones siguientes; las marcadas como en desuso se eliminará en un futuro release del paquete de compilación.  Consulte [Declaración de soporte de Microsoft para LTS y releases actuales](https://www.microsoft.com/net/core/support).

### Herramientas project.json (en desuso)

| Versión de .NET SDK        | Valor pred. |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   No    |

### Herramientas MSBuild SDK

| Versión de .NET SDK        | Valor pred. |
|-------------------------|---------|
| 1.0.3                   |   No    |
| 1.0.4                   |   Sí   |
| 1.1.0-preview1-005051   |   No    |
| 2.0.0-preview1-005977   |   No    |
| 2.0.0-preview2-006497   |   No    |

### Versiones de .NET Core Runtime

| Versión de .NET Core Runtime | Tipo de release  | Valor pred. |
|---------------------------|---------------|---------|
| 1.0.3 (en desuso)         | LTS           |   No    |
| 1.0.4 (en desuso)         | LTS           |   No    |
| 1.0.5                     | LTS           |   Sí   |
| 1.1.0 (en desuso)         | Actual       |   No    |
| 1.1.1 (en desuso)         | Actual       |   No    |
| 1.1.2                     | Actual       |   No    |
| 2.0.0-preview1-002111-00  | LTS (vista previa) |   No    |
| 2.0.0-preview2-25407-01   | LTS (vista previa) |   No    |

## Especificación de la versión de .NET SDK

Controle la versión de .NET SDK con un global.json opcional en el directorio raíz de la aplicación. Por ejemplo:
```
   {
      "sdk": {
        "version": "2.0.0-preview2-006497"
      }
   }
```
{: codeblock}

Si no se especifica, se utilizan las herramientas MSBuild correspondientes al tiempo de ejecución de GA de soporte a largo plazo (LTS) más reciente.  Para utilizar herramientas project.json, puede especificar una de las versiones de project.json arriba mencionadas, pero tenga en cuenta que estas versiones se retirarán en el futuro.
