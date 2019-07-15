---

copyright:
  years: 2016, 2018
lastupdated: "2018-07-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Lavora offline con Node.js
{: #offline_mode}

Quando un'applicazione Node.js viene trasmessa a {{site.data.keyword.Bluemix}} il pacchetto di build SDK for Node.js
normalmente scarica le risorse utente dalle risorse esterne come i moduli di Node da NPM.  In alcune
situazione, come con  [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) e
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), puoi personalizzare l'accesso ai siti esterni a {{site.data.keyword.Bluemix_notm}}.  
{: shortdesc}

Il pacchetto di build Node.js può accedere ai seguenti siti esterni. Potresti dover *consentire* questi siti
negli ambienti [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) e
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) {{site.data.keyword.Bluemix_notm}}.

* http://nodejs.org/ può essere utilizzato per verificare le versioni del motore del nodo disponibili.
* https://s3pository.heroku.com è utilizzato per richiamare le versioni del motore Node non incluse nel pacchetto di build.
*  https://www.npmjs.com/package/npm e https://semver.herokuapp.com sono utilizzati per richiamare le versioni di npm non incluse nel pacchetto di build.
* https://iojs.org è utilizzato per richiamare la vecchia versione del nodo che non era contenuta nel pacchetto di build o non era disponibile all'indirizzo  https://semver.herokuapp.com.
* https://registry.npmjs.org è utilizzato per richiamare i moduli del nodo come express.

Per ridurre la serie di siti consentiti, configura le tue applicazioni in modo da utilizzare una versione del motore Node inclusa nel pacchetto di build SDK for Node.js.  Consulta gli [ultimi aggiornamenti](./updates.html) per la serie delle versioni del motore Node incluse nel pacchetto di build.  Se configuri la tua applicazione per utilizzare queste versioni del motore Node, è necessario solo il sito https://registry.npmjs.org per scaricare i moduli.

Fai attenzione che quando vengono installate le nuove versioni del pacchetto di build SDK for Node.js la serie di versioni del motore viene spesso modificata con le versioni più recenti.  Potrebbe essere necessario riconfigurare la tua applicazione per specificare una versione del motore Node più recente inclusa nel pacchetto di build.


## Applicazioni offline
{: #offline_applications}

Per eliminare la necessità di accedere a https://registry.npmjs.org puoi includere tutti i moduli Node richiesti dalla tua applicazione all'interno dell'applicazione.  Per fare ciò esegui `npm install` per tutti i moduli dell'applicazione richiesti e includi la risultante directory `node_modules` con la tua applicazione trasmessa.

Le tue dipendenze possono avere dipendenze, che hanno dipendenze e così via, ma il `package.json`
contiene solo le dipendenze di livello superiore. Se una delle dipendenze utilizza un intervallo nel package.json e ne viene rilasciata una nuova versione, i moduli nella tua directory `node_modules` possono diventare obsoleti. *Shrinkwrap* ti aiuta a bloccare tutte le versioni delle dipendenze in modo che questo non succeda.  Per utilizzare shrinkwrap avvia una directory `node_modules` vuota o pulita. Quindi, nella directory root del tuo progetto immetti i seguenti comandi: 

```
npm install
```
{: codeblock}

```
npm dedupe
```
{: codeblock}

```
npm shrinkwrap
```
{: codeblock}

Questo può modificare il tuo `package.json` e aggiungere `npm-shrinkwrap.json` nella tua directory root.
Ogni volta che effettui una modifica alle dipendenze nel file `package.json`, riesegui i comandi `npm dedupe` e `shrinkwrap`.

## Gestione di un proxy
{: #working_with_proxy}

In alcuni ambienti come [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) e
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), può essere configurato un proxy. Consulta
[Gestione di un proxy](/docs/manageapps/workingWithProxy.html) per ulteriori dettagli.
