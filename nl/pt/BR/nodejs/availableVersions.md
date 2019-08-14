---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
subcollection: "Nodejs"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Versões disponíveis
{: #available_versions}

O {{site.data.keyword.Bluemix}} fornece todos [os tempos de execução do Node.js atualmente disponíveis](http://nodejs.org/dist/). Dos tempos de execução disponíveis, o {{site.data.keyword.IBM_notm}} fornece versões específicas que contêm aprimoramentos e correções de erros. Consulte [Atualizações mais recentes para o buildpack Node.js](/docs/runtimes/nodejs/updates.html) para obter mais informações sobre as versões suportadas.
{: shortdesc}

O buildpack Node.js da IBM armazena em cache as versões de tempo de execução do {{site.data.keyword.IBM_notm}}. Se
você usar o tempo de execução do {{site.data.keyword.IBM_notm}} SDK para Node.js em seu aplicativo, ele executará mais rápido quando você enviá-lo por push para {{site.data.keyword.Bluemix_notm}}.

## Especificando uma versão

* Use o parâmetro **node** na seção **engines** no arquivo **package.json** para especificar a versão do tempo de execução Node.js que você deseja executar.

* Se você precisar especificar uma versão do `npm` diferente da versão empacotada com o Node.js, use o parâmetro `npm` na seção `Mecanismos` no arquivo `package.json`.  

Consulte o exemplo a seguir:

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}

**Nota:** sempre especifique uma versão do nó no arquivo `package.json`. Se uma versão não for especificada, a versão do nó mais recente será usada.
