---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-18"

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

{{site.data.keyword.Bluemix}} fornece um aplicativo iniciador Node.js.  O aplicativo iniciador Node.js é um app Node.js simples que fornece um modelo que você pode usar para seu app. É possível experimentar o app iniciador, fazendo e enviando mudanças por push para o ambiente
Bluemix. Consulte [Usando os aplicativos iniciadores](/docs/cfapps/starter_app_usage.html) para obter ajuda sobre o uso do
aplicativo iniciador.

## App Management
{: #app_management}
{{site.data.keyword.Bluemix}} fornece vários utilitários para gerenciar e depurar seu app Node.js.  Consulte [Gerenciamento de App](/docs/manageapps/app_mng.html) para obter detalhes completos.

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Node.js ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://nodejs.org)
* [IBM API Connect](https://strongloop.com/)
