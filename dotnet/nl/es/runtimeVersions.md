---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versiones de tiempo de ejecución
{: #runtime_versions}

## Versiones soportadas
{: #supported_versions}

Este paquete de compilación da soporte a las versiones siguientes; las marcadas como en desuso se eliminará en un futuro release del paquete de compilación.  Consulte [Declaración de soporte de Microsoft para LTS y releases actuales](https://www.microsoft.com/net/core/support).

### Herramientas project.json (en desuso)

| Versión de .NET SDK        | Valor predeterminado |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   No    |

### Herramientas MSBuild SDK

| Versión de .NET SDK        | Valor predeterminado          |
|-------------------------|------------------|
| 2.1.301                 |   Sí            |
| 2.1.300                 |   No             |
| 2.1.201                 |   No             |
| 2.0.3                   |   No             |
| 2.0.2                   |   No             |
| 1.1.9                   |   No             |
| 1.0.4                   |   No             |


### Versiones de .NET Core Runtime

| Versión de .NET Core Runtime | Tipo de release      |
|---------------------------|-------------------|
| 2.1.1                     | LTS               |
| 2.1.0                     | LTS               |
| 2.0.7                     | LTS               |
| 2.0.3                     | Actual           |
| 2.0.2                     | Actual           |
| 2.0.0                     | LTS               |
| 1.1.8                     | LTS               |
| 1.1.2                     | LTS               |
| 1.0.11                    | LTS               |
| 1.0.5                     | LTS               |
| 1.0.4                     | LTS               |

## Especificación de la versión de .NET SDK

Controle la versión de .NET SDK con un archivo `global.json` opcional en el directorio raíz de la aplicación. Por ejemplo:
```
   {
      "sdk": {
        "version": "2.1.301"
      }
   }
```
{: codeblock}

Si no se especifica, se utiliza la última herramienta MSBuild.  Para utilizar el conjunto de herramientas project.json, puede especificar una de las versiones de project.json listadas, pero tenga en cuenta que estas versiones se eliminarán en el futuro.  Si la versión especificada no está incluida en el paquete de compilación, se utiliza la versión predeterminada, y aparece un aviso en los registros de transferencia.
