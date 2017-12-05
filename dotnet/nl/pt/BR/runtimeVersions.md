---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Versões de runtime
{: #runtime_vertsions}


{: shortdesc}

## Versões suportadas
{: #supported_versions}
Esse buildpack suporta as versões a seguir; aquelas marcadas como descontinuadas serão removidas em uma liberação de buildpack futura.  Veja [Instrução de suporte da Microsoft para liberações LTS e atuais](https://www.microsoft.com/net/core/support).

### Conjunto de ferramentas project.json (descontinuado)

| Versão SDK .NET        | Padrão |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   Não    |

### Conjunto de ferramentas SDK MSBuild

| Versão SDK .NET        | Padrão |
|-------------------------|---------|
| 1.0.3                   |   Não    |
| 1.0.4                   |   Sim   |
| 1.1.0-preview1-005051   |   Não    |
| 2.0.0-preview1-005977   |   Não    |
| 2.0.0-preview2-006497   |   Não    |

### Versões de runtime do .NET Core

| Versão do runtime do .NET Core | Tipo de Release  | Padrão |
|---------------------------|---------------|---------|
| 1.0.3 (descontinuado)     | LTS           |   Não    |
| 1.0.4 (descontinuado)     | LTS           |   Não    |
| 1.0.5                     | LTS           |   Sim   |
| 1.1.0 (descontinuado)     | Atual       |   Não    |
| 1.1.1 (descontinuado)     | Atual       |   Não    |
| 1.1.2                     | Atual       |   Não    |
| 2.0.0-preview1-002111-00  | LTS (visualização) |   Não    |
| 2.0.0-preview2-25407-01   | LTS (visualização) |   Não    |

## Especificando a versão SDK .NET

Controle a versão .NET SDK com um global.json opcional no diretório raiz do aplicativo. Por exemplo:
```
   {
      "sdk": {
        "version": "2.0.0-preview2-006497"
      }
   }
```
{: codeblock}

Se não especificado, o conjunto de ferramentas MSBuild para o tempo de execução do Long-term-support (LTS) GA mais recente será usado. Para usar o conjunto de ferramentas project.json, é possível especificar uma das versões project.json listadas acima, mas também será necessário lembrar-se de que essas versões serão removidas no futuro.
