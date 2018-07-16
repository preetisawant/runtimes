---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versiones de tiempo de ejecución
{: #runtime_versions}


{: shortdesc}

## Versiones soportadas
{: #supported_versions}

Este paquete de compilación da soporte a las versiones siguientes; las marcadas como en desuso se eliminará en un futuro release del paquete de compilación.  Consulte [Declaración de soporte de Microsoft para LTS y releases actuales](https://www.microsoft.com/net/core/support).

### Herramientas project.json (en desuso)

| Versión de .NET SDK        | Valor pred. |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   No    |

### Herramientas MSBuild SDK

| Versión de .NET SDK        | Valor pred.          |
|-------------------------|------------------|
| 1.0.4                   |   No             |
| 1.1.0                   |   Sí (solo F#)  |
| 2.0.0                   |   Sí            |

### Versiones de .NET Core Runtime

| Versión de .NET Core Runtime | Tipo de release      |
|---------------------------|-------------------|
| 1.0.4 (en desuso)        | LTS               |
| 1.0.5                     | LTS               |
| 1.1.1 (en desuso)        | LTS               |
| 1.1.2                     | LTS               |
| 2.0.0-preview2-25407-01   | Actual (vista previa) |
| 2.0.0                     | Actual           |

## Especificación de la versión de .NET SDK

Controle la versión de .NET SDK con un archivo `global.json` opcional en el directorio raíz de la aplicación. Por ejemplo:
```
   {
      "sdk": {
        "version": "2.0.0"
      }
   }
```
{: codeblock}

Si no se especifica, se utiliza la última herramienta MSBuild.  Para utilizar el conjunto de herramientas project.json, puede especificar una de las versiones de project.json listadas, pero tenga en cuenta que estas versiones se eliminarán en el futuro.  Si la versión especificada no está incluida en el paquete de compilación, se utiliza la versión predeterminada, y aparece un aviso en los registros de transferencia.
