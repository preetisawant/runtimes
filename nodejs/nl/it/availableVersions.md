---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Versioni disponibili
{: #available_versions}

{{site.data.keyword.Bluemix}} fornisce tutti [i runtime Node.js al momento disponibili](http://nodejs.org/dist/). Dei runtime disponibili, {{site.data.keyword.IBM_notm}} fornisce delle versioni specifiche contenenti miglioramenti e correzioni di bug. Per ulteriori informazioni, consulta [Aggiornamenti più recenti al pacchetto di build Node.js](/docs/runtimes/nodejs/updates.html) per ulteriori informazioni sulle versioni supportate.
{: shortdesc}

Il pacchetto di build IBM Node.js memorizza in cache le versioni di runtime di {{site.data.keyword.IBM_notm}}. Se utilizzi il runtime {{site.data.keyword.IBM_notm}} SDK for Node.js nella tua applicazione, essa viene eseguita più velocemente quando la trasmetti a {{site.data.keyword.Bluemix_notm}}.

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
