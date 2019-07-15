---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-03"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Esercitazione introduttiva
{: #getting_started}

* {: download} Congratulazioni, hai distribuito un'applicazione di esempio Hello World su {{site.data.keyword.Bluemix}}!  Per iniziare, segui questa guida dettagliata. O <a class="xref" href="http://bluemix.net" target="_blank" title="(Scarica il codice di esempio)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Scarica codice di esempio" />scarica codice di esempio</a> o esplora da solo.

Seguendo questa esercitazione introduttiva, configurerai un ambiente di sviluppo, distribuirai un'applicazione localmente e in {{site.data.keyword.Bluemix}} e integrerai un servizio database {{site.data.keyword.Bluemix}} nella tua applicazione.

## Prima di cominciare
{: #prereqs}

Avrai bisogno di quanto segue:
* [Account {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [CLI {{site.data.keyword.Bluemix_notm}}](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://git-scm.com/downloads){: new_window}
* Installa .NET Core 1.1 SDK 1.0.4 dalle istruzioni del [sito web dot.net ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.microsoft.com/net/download/core).

## Passo 1: Clona l'applicazione di esempio
{: #clone}

Per prima cosa, clona il repository GitHub dell'applicazione di esempio.
  ```
git clone https://github.com/IBM-Cloud/get-started-aspnet-core
  ```
  {: codeblock}


## Passo 2: Esegui l'applicazione localmente
{: #run_locally}

1. Nella riga di comando, modifica la directory in cui è ubicata l'applicazione di esempio.

  ```
  cd get-started-aspnet-core/src/GetStartedDotnet
  ```
  {: codeblock}

1. Esegui l'applicazione localmente eseguendo questi comandi.

  ```
dotnet restore
  ```
  {: codeblock}

  ```
dotnet run
  ```
  {: codeblock}

1. Visualizza la tua applicazione a: http://localhost:5000/.

## Passo 3: Prepara l'applicazione per la distribuzione
{: #prepare}

Per distribuire a {{site.data.keyword.Bluemix_notm}}, può essere utile impostare un file manifest.yml. Il manifest.yml include le informazioni di base sulla tua applicazione, come il nome, quanta memoria allocare per ogni istanza e la rotta. Abbiamo fornito un file manifest.yml di esempio nella directory `get-started-dotnet`.

Apri il file manifest.yml e modifica `name` da `GetStartedDotnet` con il nome della tua applicazione, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedDotnet
   random-route: true
   memory: 512M
  ```
  {: codeblock}

In questo file manifest.yml, **`random-route: true`** genera una rotta casuale per la tua applicazione per evitare il conflitto con altre rotte.  Se scegli di farlo, puoi sostituire **`random-route: true`** con **`host: myChosenHostName`**, fornendo un nome host di tua scelta.
{: tip}

## Passo 4: Distribuisci l'applicazione
{: #deploy}

Puoi utilizzare la CLI {{site.data.keyword.Bluemix_notm}} per distribuire le applicazioni.

1. Esegui l'accesso al tuo account {{site.data.keyword.Bluemix_notm}} e seleziona un endpoint API.
  ```
ibmcloud login
  ```
  {: codeblock}

  Se hai un ID utente federato, usa invece il seguente comando per eseguire l'accesso con il tuo ID SSO (single sign-on). Consulta [Accesso con un ID federato](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) per ulteriori informazioni.
 ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Indica come destinazione un'organizzazione e uno spazio Cloud Foundry:
  ```
ibmcloud target --cf
  ```
  {: codeblock}

  Se non hai un'organizzazione o uno spazio configurati, consulta [Aggiunta di organizzazioni e spazi](https://console.bluemix.net/docs/account/orgs_spaces.html).
  {: tip}

1. **Assicurati di essere nella directory principale, `get-started-aspnet-core`,  per la tua applicazione** esegui quindi il push della tua applicazione a {{site.data.keyword.Bluemix_notm}}:
  ```
ibmcloud cf push
  ```
  {: codeblock}

  Ci può volere un minuto. Se si verifica un errore nel processo di distribuzione, puoi utilizzare il comando `ibmcloud cf logs. <Your-App-Name> --recent` per risolverlo.

Quando la distribuzione è stata completata, dovresti vedere un messaggio che indica che la tua applicazione è in esecuzione.  Visualizza la tua applicazione all'URL elencato nell'output del comando trasmesso.  Puoi anche immettere il seguente comando per visualizzare lo stato della tua applicazioni e vedere l'URL.
  ```
ibmcloud cf apps
  ```
  {: codeblock}

## Passo 5: Collegati a un database MySQL
{: connect_mysql}

Successivamente, aggiungeremo un database ClearDB MySQL a questa applicazione e la configureremo in modo che possa essere eseguita localmente e su {{site.data.keyword.Bluemix_notm}}.

1. Nel tuo browser, accedi a {{site.data.keyword.Bluemix_notm}} e passa al dashboard. Seleziona **Crea risorsa**.
2. Scegli la sezione **Data and Analytics** e seleziona **ClearDB Managed MySQL Database** e crea il tuo servizio.
3. Passa alla vista **Connessioni** e seleziona la tua applicazione, quindi **Crea connessione**.
4. Seleziona **Riprepara** quando richiesto. {{site.data.keyword.Bluemix_notm}} riavvierà la tua applicazione e fornirà le credenziali del database alla tua applicazione utilizzando la variabile di ambiente `VCAP_SERVICES`. Questa variabile di ambiente è disponibile per l'applicazione solo quando è in esecuzione su {{site.data.keyword.Bluemix_notm}}.

Le variabili di ambiente ti abilitano a separare le impostazioni di distribuzione dal tuo codice di origine. Ad esempio, invece di impostare come hardcoded una password del database, puoi archiviarla in una variabile di ambiente di riferimento nel tuo codice di origine.
{: tip}

## Passo 6: Utilizza il database localmente
{: #use_database}

Ora aggiorneremo il tuo codice locale per puntare a questo database. Archivieremo le credenziali per i servizi in un file JSON. Questo file sarà utilizzato SOLO quando l'applicazione è in esecuzione localmente. Quando è in esecuzione in {{site.data.keyword.Bluemix_notm}}, le credenziali saranno lette dalla variabile di ambiente VCAP_SERVICES.

1. Crea il file src/GetStartedDotnet/vcap-local.json

2. Nel tuo browser, vai al dashboard {{site.data.keyword.Bluemix_notm}} e seleziona **_la_tua_applicazione_ > Connessioni**. Fai clic sull'icona del menu {{site.data.keyword.cloudant_short_notm}} (**&vellip;**) e seleziona **Visualizza credenziali**.

3. Copia e incolla l'oggetto json completo dalle credenziali nel file `vcap-local.json` e salva le modifiche.  Il risultato sarà qualcosa di simile al seguente esempio:
  ```
  {
  "cleardb": [
    {
      "credentials": {
        ...
        "uri": "mysql://user:password@some-hostname.cleardb.net:3306/database-name?reconnect=true",
        ...
      },
      ...
      "name": "My ClearDB service instance name",
      ...
    }
  ]
}
  ```

4. Dalla directory `get-started-aspnet-core/src/GetStartedDotnet` riavvia la tua applicazione con il comando `dotnet run`.

Aggiorna la tua vista del browser all'indirizzo: http://localhost:5000/. Tutti i nomi immessi nell'applicazione saranno ora aggiunti al database.

La tua applicazione locale e {{site.data.keyword.Bluemix_notm}} stanno condividendo il database.  Visualizza la tua applicazione {{site.data.keyword.Bluemix_notm}} all'URL elencato nell'output del comando trasmesso precedentemente.  I nomi che aggiungi dall'applicazione dovrebbero essere visualizzati entrambi quando aggiorni i browser.

Ricorda: se non hai bisogno della tua applicazione live, arrestala così da non incorrere in alcun addebito non previsto.
{: tip}

## Passi successivi

* [Esercitazioni](/docs/tutorials/index.html)
* [Esempi ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
