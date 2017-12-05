---

copyright:
  years: 2015, 2017
lastupdated: "2017-06-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Versões disponíveis
{: #available_versions}

O {{site.data.keyword.Bluemix}} fornece todos [os tempos de execução do Node.js atualmente disponíveis](http://nodejs.org/dist/). Dos tempos de execução disponíveis, a IBM fornece versões específicas que contêm aprimoramentos e correções de bug. Veja [Atualizações mais recentes para o buildpack do Node.js](/docs/runtimes/nodejs/updates.html) para obter mais informações sobre as versões suportadas.
{: shortdesc}

O buildpack IBM Node.js armazena em cache as versões de tempo de execução da IBM. Se você usar o tempo de execução do IBM SDK for Node.js em seu aplicativo, o aplicativo será executado mais rápido quando enviá-lo por push para o Bluemix.

## Especificando uma versão

* Use o parâmetro **node** na seção **engines** no arquivo **package.json** para especificar a versão do tempo de execução Node.js que você deseja executar.

* Se você precisar especificar uma versão de npm diferente da versão empacotada com o Node.js, use o parâmetro **npm** na seção **engines** no arquivo **package.json**.  

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

**Nota:** uma versão do nó deve sempre ser especificada no arquivo **package.json**. Se não for, a versão do nó mais recente será usada.
