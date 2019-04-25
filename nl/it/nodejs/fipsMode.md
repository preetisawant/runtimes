---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Modalità FIPS
{: #fips_mode}

Le versioni del pacchetto di build Node.js da v3.2-20160315-1257 a v3.20.2-20180523-1639 supportano [FIPS ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards).  
{: shortdesc}

**Il modulo FIPS OpenSSL è obsoleto:** come per il pacchetto di build Node.js v3.22, il modulo FIPS OpenSSL non è più disponibile nelle versioni 6.x e 8.x del runtime. Solo la versione 4.x continua ad includere il modulo FIPS OpenSSL. Ulteriori informazioni in [Aggiornamenti più recenti al pacchetto di build Node.js](updates.html#fips-deprecation).

Per utilizzare un nodo abilitato FIPS imposta la variabile di ambiente FIPS_MODE su true.
Ad esempio:

```
    ibmcloud cf set-env myapp FIPS_MODE true
```
{: codeblock}

È importante comprendere che quando FIPS_MODE è true alcuni moduli del nodo hanno esito negativo.  Ad esempio, i **moduli del nodo che utilizzano [MD5 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://en.wikipedia.org/wiki/MD5) avranno esito negativo**, come [Express ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://expressjs.com/).  Per Express, l'impostazione di [etag ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://expressjs.com/en/api.html) su
false nella tua applicazione Express può aiutare ad aggirare questo problema. Ad esempio puoi eseguire quanto segue nel tuo codice:
```
    app.set('etag', false);
```
{: codeblock}
Consulta questo [post stackoverflow ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)
per ulteriori informazioni.

**NOTA** [Gestione applicazioni](../common/app_mng.html) e FIPS_MODE *NON* sono supportati contemporaneamente.  Se la variabile di ambiente BLUEMIX_APP_MGMT_ENABLE è configurata e le variabili di ambiente FIPS_MODE sono impostate su true, la preparazione dell'applicazione avrà esito negativo.

Esistono vari metodi per controllare lo stato di FIPS_MODE:
<ul>
<li> Puoi controllare i log della tua applicazione per un messaggio simile al seguente:    

  <pre>
  Installing FIPS-enabled IBM SDK for Node.js (4.4.3) from cache
  </pre>
  {: codeblock}

Questo messaggio indica che un motore node.js abilitato FIPS è in esecuzione ma non necessariamente che FIPS sia in esecuzione.
</li>

<li> Puoi controllare il valore di **process.versions.openssl**. Ad esempio:

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

Se la versione SSL contiene "fips", la versione di SSL utilizzata supporta FIPS.  
</li>

<li> Per node.js versione 6 o successiva, puoi controllare il valore restituito da crypto.fips in codice come nel seguente esempio:

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

Se il valore restituito è 1, FIPS è in utilizzo. Nota che crypto.fips restituirà *undefined* per le versioni di node.js precedenti alla 6.
</li>
</ul>

## Nodejs v4
{: #nodejs_v4_fips}

La seguente tabella illustra il funzionamento di node.js v4 con FIPS:

|                 | Risultato        |
| :-------------- | :------------ |
|FIPS_MODE=true   |positivo (1)    |
|FIPS_MODE !=true |positivo (2)    |

* positivo (1)
  * FIPS è in utilizzo.
  * I log includeranno il messaggio *Installing FIPS-enabled IBM SDK for Node.js*.
  * Il valore restituito da process.versions.openssl conterrà "fips".
* positivo (2)
  * FIPS *NON* è in utilizzo.
  * Il log *NON* includerà il messaggio *Installing FIPS-enabled IBM SDK for Node.js*.
  * Il valore restituito da process.versions.openssl *NON* conterrà "fips".

## Node.js v6 e successiva
{: #nodejs_v6_fips}

Per eseguire la modalità FIPS con Node.js versione 6 e successiva in aggiunta all'impostazione **FIPS_MODE=true**, devi inoltre includere
**--enable-fips** nel tuo comando di avvio come nel seguente esempio:
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

La seguente tabella illustra il funzionamento di node.js v6 e successiva con FIPS.

|                 |--enable-fips  |NO --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |positivo (1)    |positivo (2)      |
|FIPS_MODE !=true |non riuscito (3)    |positivo (4)      |

* positivo (1)
  * FIPS è in utilizzo.
  * I log includeranno il messaggio *Installing FIPS-enabled IBM SDK for Node.js*.
  * Il valore restituito da process.versions.openssl conterrà "fips"
  * crypto.fips restituirà 1, che indica che FIPS è in utilizzo
* positivo (2)
  * FIPS *NON* è in utilizzo.
  * I log includeranno il messaggio *Installing FIPS-enabled IBM SDK for Node.js*.
  * Il valore restituito da process.versions.openssl conterrà "fips"
  * crypto.fips restituirà 0, che indica che FIPS *NON* è in utilizzo
* non riuscito (3)
  * FIPS *NON* è in utilizzo.
  * Il log *NON* includerà il messaggio *Installing FIPS-enabled IBM SDK for Node.js*.
  * staging avrà esito negativo con il messaggio "ERR node: bad option: --enable-fips"
* positivo (4)
  * FIPS *NON* è in utilizzo.
  * Il log *NON* includerà il messaggio *Installing FIPS-enabled IBM SDK for Node.js*.
  * Il valore restituito da process.versions.openssl *NON* conterrà "fips"
  * crypto.fips restituirà 0, che indica che FIPS *NON* è in utilizzo
