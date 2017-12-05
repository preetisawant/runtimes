---

copyright:
  years: 2015, 2017
lastupdated: "2017-06-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Versioni disponibili
{: #available_versions}

{{site.data.keyword.Bluemix}} fornisce tutti [i runtime Node.js al momento disponibili](http://nodejs.org/dist/). Dei runtime disponibili, IBM fornisce delle versioni specifiche contenenti miglioramenti e correzioni di bug. Per ulteriori informazioni, consulta [Aggiornamenti più recenti al pacchetto di build Node.js](/docs/runtimes/nodejs/updates.html) per ulteriori informazioni sulle versioni supportate.
{: shortdesc}

Il pacchetto di build IBM Node.js memorizza in cache le versioni di runtime di IBM. Se utilizzi il runtime IBM SDK for Node.js nella tua applicazione, essa viene eseguita più velocemente quando la trasmetti a Bluemix.

## Specifica una versione

* Utilizza il parametro **node** nella sezione **engines** nel file **package.json** per specificare la versione di runtime Node.js che vuoi eseguire.

* Se hai bisogno di specificare una versione di npm diversa da quella integrata in Node.js, utilizza il parametro **npm** nella sezione **engines** nel file **package.json**.  

Guarda il seguente esempio:

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

**Nota:** nel file **package.json** deve essere sempre specificata una versione di nodo. In caso contrario, viene utilizzata la versione di nodo più recente.
