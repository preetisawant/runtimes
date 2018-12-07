---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-24"

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
{: #getting-started}

* {: download} Congratulazioni, hai distribuito un'applicazione di esempio Hello World su {{site.data.keyword.Bluemix}}!  Per iniziare, segui questa guida dettagliata. O <a class="xref" href="http://bluemix.net" target="_blank" title="(Scarica il codice di esempio)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Scarica codice di esempio" />scarica codice di esempio</a> o esplora da solo.

Seguendo questa esercitazione introduttiva Liberty for Java, configurerai un ambiente di sviluppo, distribuirai un'applicazione localmente e in {{site.data.keyword.Bluemix}} e integrerai un servizio database nella tua applicazione.

In questi documenti, i riferimenti alla CLI Cloud Foundry sono ora aggiornati alla CLI {{site.data.keyword.Bluemix_notm}}. La CLI {{site.data.keyword.Bluemix_notm}} ha gli stessi familiari comandi Cloud Foundry ma con una migliore integrazione con gli account {{site.data.keyword.Bluemix_notm}} e altri servizi. Scopri ulteriori informazioni introduttive alla CLI {{site.data.keyword.Bluemix_notm}} in questa esercitazione.
{: tip}

## Prima di cominciare
{: #prereqs}

Ti serviranno i seguenti account e strumenti:
* [Account {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [CLI {{site.data.keyword.Bluemix_notm}}](../../cli/reference/ibmcloud/download_cli.html)
* [Git ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://git-scm.com/downloads){: new_window}
* [Maven ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://maven.apache.org/download.cgi){: new_window}

## Passo 1: Clona l'applicazione di esempio
{: #clone}

Per prima cosa, clona il repository GitHub dell'applicazione di esempio.

  ```
git clone https://github.com/IBM-Cloud/get-started-java
  ```
  {: codeblock}


## Passo 2: Esegui l'applicazione localmente utilizzando la riga di comando
{: #run_locally}

Utilizza Maven per creare il tuo codice sorgente ed eseguire l'applicazione risultante.

1. Nella riga di comando, modifica la directory in cui è ubicata l'applicazione di esempio.

  ```
cd get-started-java
  ```
  {: codeblock}

1. Utilizza Maven per installare le dipendenze e creare il file .war.

  ```
mvn clean install
  ```
  {: codeblock}

1. Esegui l'applicazione localmente su Liberty.

  ```
mvn install liberty:run-server
  ```
  {: codeblock}

Quando visualizzi il messaggio *The server defaultServer is ready to run a smarter planet.*, puoi visualizzare la tua applicazione all'indirizzo: http://localhost:9080/GetStartedJava.

Per arrestare la tua applicazione, premi **Ctrl-C** nella finestra della riga di comando in cui hai avviato l'applicazione.

## Passo 3: Prepara l'applicazione per la distribuzione
{: #prepare}

Per distribuire a {{site.data.keyword.Bluemix_notm}}, può essere utile impostare un file manifest.yml. Il manifest.yml include le informazioni di base sulla tua applicazione, come il nome, quanta memoria allocare per ogni istanza e la rotta. Abbiamo fornito un file manifest.yml di esempio nella directory `get-started-java`.

Apri il file manifest.yml e modifica `name` da `GetStartedJava` con il nome della tua applicazione, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

In questo file manifest.yml, **random-route: true** genera una rotta casuale per la tua applicazione per evitare il conflitto con altre rotte.  Se scegli di farlo, puoi sostituire **random-route: true** con **host: myChosenHostName**, fornendo un nome host di tua scelta.
{: tip}

## Passo 4: Distribuisci a {{site.data.keyword.Bluemix_notm}}
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

1. Dall'interno della directory `get-started-java`, trasmetti la tua applicazione a {{site.data.keyword.Bluemix_notm}}.

  ```
ibmcloud cf push
  ```
  {: codeblock}

La distribuzione della tua applicazione può impiegare diversi minuti. Quando la distribuzione è stata completata, visualizzerai un messaggio che la tua applicazione è in esecuzione. Visualizza la tua applicazione all'URL elencato nell'output del comando trasmesso o visualizza l'URL e lo stato di distribuzione dell'applicazione eseguendo il seguente comando:

  ```
ibmcloud cf apps
  ```
  {: codeblock}

Puoi risolvere gli errori nel processo di distribuzione eseguendo il comando `ibmcloud cf logs <Your-App-Name> --recent`.
{: tip}  

## Passo 5: Aggiungi un database
{: #add_database}

Successivamente, aggiungeremo un database NoSQL {{site.data.keyword.cloudant_short_notm}} a questa applicazione e la configureremo in modo che possa essere eseguita localmente e su {{site.data.keyword.Bluemix_notm}}.

1. Nel tuo browser, accedi a {{site.data.keyword.Bluemix_notm}} e passa al dashboard. Seleziona **Crea risorsa**.
1. Cerca **{{site.data.keyword.cloudant_short_notm}}** e seleziona il servizio.
1. Per **Metodi di autenticazione disponibili**, seleziona **Utilizza sia credenziali legacy che IAM**. Puoi lasciare le impostazioni predefinite per gli altri campi. Fai clic su **Crea** per creare il servizio.
1. Nella navigazione, vai a **Connessioni**. Seleziona la tua applicazione e fai clic su **Crea connessione**.
1. Connetti la tua applicazione utilizzando i valori predefiniti e fai clic su **Collega e riprepara l'applicazione**. Quindi, quando ti viene richiesto, fai clic su **Riprepara**.

   {{site.data.keyword.Bluemix_notm}} riavvierà la tua applicazione e fornirà le credenziali del database alla tua applicazione utilizzando la variabile di ambiente `VCAP_SERVICES`. Questa variabile di ambiente è disponibile per l'applicazione solo quando è in esecuzione su {{site.data.keyword.Bluemix_notm}}.

Le variabili di ambiente ti abilitano a separare le impostazioni di distribuzione dal tuo codice sorgente. Ad esempio, invece di impostare come hardcoded una password del database, puoi memorizzarla in una variabile di ambiente a cui fai riferimento nel tuo codice sorgente.
{: tip}

## Passo 6: Utilizza il database
{: #use_database}
Ora aggiorneremo il tuo codice locale per puntare a questo database. Archivieremo le credenziali per i servizi in un file properties. Questo file sarà utilizzato SOLO quando l'applicazione è in esecuzione localmente. Quando è in esecuzione in {{site.data.keyword.Bluemix_notm}}, le credenziali saranno lette dalla variabile di ambiente `VCAP_SERVICES`.

1. Nel tuo browser, vai al dashboard {{site.data.keyword.Bluemix_notm}} e seleziona **_la_tua_applicazione_ > Connessioni**. Fai clic sull'icona del menu {{site.data.keyword.cloudant_short_notm}} (**&vellip;**) e seleziona **Visualizza credenziali**.

2. Copia e incolla solo l'`url` dalle credenziali nel campo `url` del file `src/main/resources/cloudant.properties` e salva le modifiche.

  ```
cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:codeblock}

3. Riavvia il server.

Aggiorna la tua vista del browser all'indirizzo http://localhost:9080/GetStartedJava/. Qualsiasi nome immetti nell'applicazione verrà ora aggiunto al database.

La tua applicazione locale e {{site.data.keyword.Bluemix_notm}} stanno condividendo il database. I nomi che aggiungi dall'applicazione saranno visualizzati entrambi quando aggiorni i browser.

Ricorda, se non hai bisogno della tua applicazione live su {{site.data.keyword.Bluemix_notm}}, arrestala così da non incorrere in alcun addebito non previsto.
{: tip}  

## Passi successivi

* [Esercitazioni](/docs/tutorials/index.html)
* [Esempi ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
