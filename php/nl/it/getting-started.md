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

Seguendo questa esercitazione introduttiva, configurerai un ambiente di sviluppo, distribuirai un'applicazione localmente e in {{site.data.keyword.Bluemix}} e integrerai un servizio database nella tua applicazione.

In questi documenti, i riferimenti alla CLI Cloud Foundry sono ora aggiornati alla CLI {{site.data.keyword.Bluemix_notm}}. La CLI {{site.data.keyword.Bluemix_notm}} ha gli stessi familiari comandi Cloud Foundry ma con una migliore integrazione con gli account {{site.data.keyword.Bluemix_notm}} e altri servizi. Scopri ulteriori informazioni introduttive alla CLI {{site.data.keyword.Bluemix_notm}} in questa esercitazione.
{: tip}

## Prima di cominciare
{: #prereqs}

Avrai bisogno di quanto segue:
* [Account {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [CLI {{site.data.keyword.Bluemix_notm}}](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://git-scm.com/downloads){: new_window}
* [PHP ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://php.net/downloads.php){: new_window}
* [Composer ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://getcomposer.org/download/){: new_window}

## Passo 1: Clona l'applicazione di esempio
{: #clone}

Per prima cosa, clona il repository e passa alla directory dove si trova l'applicazione di esempio.

  ```
git clone https://github.com/IBM-Cloud/get-started-php
  ```
  {: codeblock}

  ```
cd get-started-php
  ```
  {: codeblock}

## Passo 2: Esegui l'applicazione localmente

1. Installa le dipendenze.

  ```
php composer.phar install
  ```
{: codeblock}

1. Esegui l'applicazione localmente.

  ```
php -S localhost:8000
  ```
  {: codeblock}

1. Visualizza la tua applicazione al seguente URL: http://localhost:8000

## Passo 3: Prepara l'applicazione per la distribuzione
{: #prepare}

Per distribuire a {{site.data.keyword.Bluemix_notm}}, può essere utile impostare un file manifest.yml. Il manifest.yml include le informazioni di base sulla tua applicazione, come il nome, quanta memoria allocare per ogni istanza e la rotta. Abbiamo fornito un file manifest.yml di esempio nella directory `get-started-php`.

Apri il file manifest.yml e modifica `name` da `GetStartedPHP` con il nome della tua applicazione, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedPHP
   random-route: true
   memory: 128M
  ```
  {: codeblock}

In questo file manifest.yml, **random-route: true** genera una rotta casuale per la tua applicazione per evitare il conflitto con altre rotte.  Se scegli di farlo, puoi sostituire **random-route: true** con **host: myChosenHostName**, fornendo un nome host di tua scelta.
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

1. Dall'interno della directory *get-started-php* trasmetti la tua applicazione a {{site.data.keyword.Bluemix_notm}}

   ```
ibmcloud cf push
   ```
   {: codeblock}

  Ci può volere un minuto. Se si verifica un errore nel processo di distribuzione, puoi utilizzare il comando `ibmcloud cf logs. <Your-App-Name> --recent` per risolverlo.

Quando la distribuzione è stata completata dovresti visualizzare un messaggio che indica che la tua applicazione è in esecuzione.  Visualizza la tua applicazione all'URL elencato nell'output del comando trasmesso. Puoi anche immettere il seguente comando per visualizzare lo stato delle tue applicazioni e vedere l'URL.

  ```
ibmcloud cf apps
  ```
  {: codeblock}

## Passo 5: Aggiungi un database
{: #add_database}

Successivamente, aggiungeremo un database NoSQL {{site.data.keyword.cloudant_short_notm}} a questa applicazione e la configureremo in modo che possa essere eseguita localmente e su {{site.data.keyword.Bluemix_notm}}.

1. Nel tuo browser, accedi a {{site.data.keyword.Bluemix_notm}} e passa al dashboard. Seleziona **Crea risorsa**.
2. Scegli la sezione **Data and Analytics** e seleziona **{{site.data.keyword.cloudant_short_notm}}** e crea il tuo servizio.
3. Passa alla vista **Connessioni** e seleziona la tua applicazione, quindi **Crea connessione**.
4. Seleziona **Riprepara** quando richiesto. {{site.data.keyword.Bluemix_notm}} riavvierà la tua applicazione e fornirà le credenziali del database alla tua applicazione utilizzando la variabile di ambiente `VCAP_SERVICES`. Questa variabile di ambiente è disponibile per l'applicazione solo quando è in esecuzione su {{site.data.keyword.Bluemix_notm}}.

Le variabili di ambiente ti abilitano a separare le impostazioni di distribuzione dal tuo codice di origine. Ad esempio, invece di impostare come hardcoded una password del database, puoi archiviarla in una variabile di ambiente di riferimento nel tuo codice di origine.
{: tip}

## Passo 6: Utilizza il database
{: #use_database}
Ora aggiorneremo il tuo codice locale per puntare a questo database. Creeremo un file .env che archivierà le credenziali per i servizi che l'applicazione utilizzerà. Questo file sarà utilizzato SOLO quando l'applicazione è in esecuzione localmente. Quando è in esecuzione in {{site.data.keyword.Bluemix_notm}}, le credenziali saranno lette dalla variabile di ambiente VCAP_SERVICES.

1. Crea un file denominato `.env` nella directory `get-started-php` con il seguente contenuto:

  ```
CLOUDANT_HOST=
  CLOUDANT_USERNAME=
  CLOUDANT_PASSWORD=
  ```
  {: codeblock}

2. Nel tuo browser, vai al dashboard {{site.data.keyword.Bluemix_notm}} e seleziona **_la_tua_applicazione_ > Connessioni**. Fai clic sull'icona del menu {{site.data.keyword.cloudant_short_notm}} (**&vellip;**) e seleziona **Visualizza credenziali**.

3. Copia e incolla i valori dei campi `CLOUDANT_HOST`, `CLOUDANT_USERNAME` e `CLOUDANT_PASSWORD` nel file `.env` e salva le modifiche.  Il risultato sarà qualcosa di simile:

  ```
CLOUDANT_HOST=abc...yz.cloudant.com
  CLOUDANT_USERNAME=abc...yz
  CLOUDANT_PASSWORD=445d...d1a
  ```
  {: codeblock}

4. Esegui la tua applicazione localmente.

  ```
php -S localhost:8000
  ```
  {: codeblock}

Visualizza la tua applicazione in: http://localhost:8000. Tutti i nomi immessi nell'applicazione saranno ora aggiunti al database.

La tua applicazione locale e {{site.data.keyword.Bluemix_notm}} stanno condividendo il database.  Visualizza la tua applicazione {{site.data.keyword.Bluemix_notm}} all'URL elencato nell'output del comando trasmesso precedentemente.  I nomi che aggiungi dall'applicazione dovrebbero essere visualizzati entrambi quando aggiorni i browser.

Ricorda: se non hai bisogno della tua applicazione live, arrestala così da non incorrere in alcun addebito non previsto.
{: tip}  

## Passi successivi

* [Esercitazioni](/docs/tutorials/index.html)
* [Esempi ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
