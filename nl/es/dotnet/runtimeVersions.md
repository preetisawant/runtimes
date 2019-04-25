---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-20"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versiones de tiempo de ejecución
{: #runtime_versions}

## Versiones soportadas
{: #supported_versions}

Este paquete de compilación da soporte a las versiones siguientes; las marcadas como en desuso se eliminará en un futuro release del paquete de compilación.  Consulte [Declaración de soporte de Microsoft para LTS y releases actuales](https://www.microsoft.com/net/core/support).


### Versión de .NET SDK

| Versión de .NET SDK        | Valor predeterminado          |
|-------------------------|------------------|
| 2.2.104                 |   Sí            |
| 2.1.504                 |   No             |
| 2.1.403                 |   No             |
| 2.0.3                   |   No             |
| 1.1.12                  |   No             |
| 1.1.11                  |   No             |
| 1.0.4                   |   No             |


### Versiones de .NET Core Runtime

| Versión de .NET Core Runtime | Tipo de release      |
|---------------------------|-------------------|
| 2.2.2                     | Actual           |  
| 2.2.1                     | LTS               |
| 2.1.8                     | LTS               |
| 2.1.7                     | LTS               |
| 2.0.9                     | LTS               |
| 2.0.7                     | LTS               |
| 1.1.11                    | LTS               |
| 1.1.10                    | LTS               |
| 1.0.12                    | LTS               |
| 1.0.11                    | LTS               |


### Versiones de .NET aspnetcore

| Versión .NET aspnetcore | Tipo de release        |
|---------------------------|-------------------|
| 2.2.2                     | Actual           |  
| 2.2.1                     | LTS               |
| 2.1.8                     | LTS               |
| 2.1.7                     | LTS               |



## Especificación de la versión de .NET SDK

Controle la versión de .NET SDK con un archivo `global.json` opcional en el directorio raíz de la aplicación. Por ejemplo:
```
   {
      "sdk": {
        "version": "2.2.104"
      }
   }
```
{: codeblock}

Si no se especifica, se utiliza la última herramienta MSBuild.  Para utilizar el conjunto de herramientas project.json, puede especificar una de las versiones de project.json listadas, pero tenga en cuenta que estas versiones se eliminarán en el futuro.  Si la versión especificada no está incluida en el paquete de compilación, se utiliza la versión predeterminada, y aparece un aviso en los registros de transferencia.
