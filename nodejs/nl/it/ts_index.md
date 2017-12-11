---

copyright:
  years: 2017
lastupdated: "2017-09-18"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Risoluzione dei problemi per SDK for Node.js
{: #ts}


Sono qui riportate le risposte alle domande comuni di risoluzione dei problemi sull'utilizzo di SDK for Node.js su {{site.data.keyword.Bluemix}}.
{:shortdesc}

## Impossibile avviare l'applicazione con un errore “Mancanza di spazio sul dispositivo”
{: #no_space_left_on_device}


Impossibile avviare un'applicazione Node.js  con un errore “Mancanza di spazio sul dispositivo”. Ad esempio, l'errore nei log può essere simile al seguente:
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

Le applicazioni Node.js che utilizzano le versioni di NPM precedenti alla 3 utilizzano più spazio per lo scaricamento delle dipendenze.
{: tsCauses}

Modifica il file package.json della tua applicazione per utilizzare la versione 3 di NPM o una superiore.
{: tsResolve}

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

## L'applicazione viene riavviata a causa di vincoli di memoria
{: #oom}

Node.js non conosce quanta memoria è disponibile per l'applicazione, per cui il raccoglitore dei dati inutilizzati potrebbe non essere stato eseguito prima dell'esaurimento della memoria.

```
2017-09-01T11:00:42.19-0400 [APP/PROC/WEB/0]OUT Exit status 137
2017-09-01T11:00:42.23-0400 [CELL/0]     OUT Exit status 0
2017-09-01T11:00:42.27-0400 [CELL/0]     OUT Destroying container
2017-09-01T11:00:42.34-0400 [API/0]      OUT Process has crashed with type: "web"
2017-09-01T11:00:42.36-0400 [API/0]      OUT App instance exited with guid eecfba3b-430c-4a6b-b71f-ac72816fe152 payload: {"instance"=>"77dbb981-16d0-3a05-3235-9a4b", "index"=>0, "reason"=>"CRASHED", "exit_description"=>"2 error(s) occurred:\n\n* 2 error(s) occurred:\n\n* Exited with status 137 (out of memory)\n* cancelled\n* cancelled", "crash_count"=>1, "crash_timestamp"=>1504278042244633291, "version"=>"6497b5b5-67d4-4c5a-b1af-362e522a029d"}
2017-09-01T11:00:43.35-0400 [CELL/0]     OUT Successfully destroyed container
```
{: codeblock}

Una possibile soluzione è di impostare l'opzione `--max_old_space_size` nel comando di avvio dell'applicazione nel file package.json. Questa opzione rappresenta parte del footprint della memoria dell'applicazione e dovrebbe essere impostata su un valore inferiore al totale di memoria disponibile per l'applicazione. Per ulteriori informazioni, consulta [Large memory spikes and Heroku](https://github.com/nodejs/node/issues/3370) per una discussione più dettagliata su questo argomento.
```
  "scripts": {
    "start": "node --max_old_space_size=800 server.js"
  }
```
{: codeblock}
