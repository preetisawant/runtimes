---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versões de runtime
{: #runtime_versions}

## Versões suportadas
{: #supported_versions}

Esse buildpack suporta as versões a seguir; aquelas marcadas como descontinuadas serão removidas em uma liberação de buildpack futura.  Veja [Instrução de suporte da Microsoft para liberações LTS e atuais](https://www.microsoft.com/net/core/support).

### Conjunto de ferramentas project.json (descontinuado)

| Versão SDK .NET        | Padrão |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   Não    |

### Conjunto de ferramentas SDK MSBuild

| Versão SDK .NET        | Padrão          |
|-------------------------|------------------|
| 2.1.301                 |   Sim            |
| 2.1.300                 |   Não             |
| 2.1.201                 |   Não             |
| 2.0.3                   |   Não             |
| 2.0.2                   |   Não             |
| 1.1.9                   |   Não             |
| 1.0.4                   |   Não             |


### Versões de runtime do .NET Core

| Versão do runtime do .NET Core | Tipo de Release      |
|---------------------------|-------------------|
| 2.1.1                     | LTS               |
| 2.1.0                     | LTS               |
| 2.0.7                     | LTS               |
| 2.0.3                     | Atual           |
| 2.0.2                     | Atual           |
| 2.0.0                     | LTS               |
| 1.1.8                     | LTS               |
| 1.1.2                     | LTS               |
| 1.0.11                    | LTS               |
| 1.0.5                     | LTS               |
| 1.0.4                     | LTS               |

## Especificando a versão SDK .NET

Controle a versão do .NET SDK com um arquivo `global.json` opcional no diretório-raiz do aplicativo. Por exemplo:
```
   {
      "sdk": {
        "version": "2.1.301"
      }
   }
```
{: codeblock}

Se não for especificado, o conjunto de ferramentas MSBuild mais recente será usado.  Para usar o conjunto de ferramentas
project.json, é possível especificar uma das versões do project.json listadas, mas lembre-se que essas versões serão
removidas no futuro.  Se a versão especificada não for incluída no buildpack, a versão padrão será usada e um aviso aparecerá nos
logs temporários.
