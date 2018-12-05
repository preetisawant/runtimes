---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Node.js
{: #nodejs_runtime}

O tempo de execução Node.js no {{site.data.keyword.Bluemix}} é desenvolvido com o buildpack sdk-for-nodejs.
O buildpack sdk-for-nodejs fornece um ambiente de tempo de execução completo para apps Node.js.
{: shortdesc}

O buildpack sdk-for-nodejs é usado quando o aplicativo contém um arquivo **package.json** no diretório-raiz.

O aplicativo deve atender na porta que é designada a ele por meio da variável de ambiente PORT.
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

## Aplicativo iniciador
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} fornece um aplicativo iniciador Node.js.  O aplicativo iniciador Node.js é um app Node.js simples que fornece um modelo que você pode usar para seu app. É possível experimentar o app iniciador e fazer e enviar mudanças por push para o ambiente do {{site.data.keyword.Bluemix_notm}}. Veja [Usando os aplicativos iniciadores](../common/starter_app_usage.html) para obter ajuda sobre o uso do aplicativo iniciador.

## App Management
{: #app_management}
{{site.data.keyword.Bluemix_notm}} fornece vários utilitários para gerenciar e depurar seu app Node.js.  Consulte [Gerenciamento de App](../common/app_mng.html) para obter detalhes completos.
