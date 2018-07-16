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
* [Eclipse IDE for Java EE Developers ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://git-scm.com/downloads){: new_window}
* [Maven ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat version 8.0.41 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}


## Passo 1: Clona l'applicazione di esempio
{: #clone}

Clona il repository e modifica la directory in cui è ubicata l'applicazione di esempio.
  ```
git clone https://github.com/IBM-Cloud/get-started-tomcat
  ```
{: codeblock}

  ```
cd get-started-tomcat
  ```
{: codeblock}

Studia i file nella directory *get-started-tomcat* per acquisire familiarità con i contenuti.

## Passo 2: Esegui l'applicazione localmente
{: #run_locally}

Devi installare le dipendenze e creare un file .war come definito nel file pom.xml per eseguire l'applicazione.

1. Installa le dipendenze.
  ```
mvn clean install  
  ```
  {: codeblock}

1. Copia GetStartedTomcat.war dalla directory `target` nella tua directory `tomcat-install-dir` `webapps`.

1. Esegui l'applicazione.  
  ```
<tomcat-install-dir>/bin/startup.bat|.sh
  ```
  {: codeblock}

1. Visualizza la tua applicazione al seguente URL: http://localhost:8080/GetStartedTomcat/

Utilizza `shutdown.bat|.sh` per arrestare la tua applicazione.  Tieni presente che potresti aver bisogno di fornire l'autorizzazione di esecuzione dei comandi.
{: tip}

## Passo 3: Prepara l'applicazione per la distribuzione a {{site.data.keyword.Bluemix_notm}}
{: #prepare}

Per distribuire a {{site.data.keyword.Bluemix_notm}}, può essere utile impostare un file manifest.yml. Il manifest.yml include le informazioni di base sulla tua applicazione, come il nome, quanta memoria allocare per ogni istanza e la rotta. Abbiamo fornito un file manifest.yml di esempio nella directory `get-started-tomcat`.

Apri il file manifest.yml e modifica `name` da `GetStartedTomcat` con il nome della tua applicazione, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/GetStartedTomcat.war
    buildpack: java_buildpack
  ```
  {: codeblock}

In questo file manifest.yml, **`random-route: true`** genera una rotta casuale per la tua applicazione per evitare il conflitto con altre rotte.  Se scegli di farlo, puoi sostituire **`random-route: true`** con **`host: myChosenHostName`**, fornendo un nome host di tua scelta.
{: tip}

## Passo 4: Distribuisci l'applicazione
{: #deploy}

Puoi utilizzare la CLI {{site.data.keyword.Bluemix_short}} per distribuire le applicazioni.

1. Esegui l'accesso al tuo account {{site.data.keyword.Bluemix_short}} e seleziona un endpoint API.

  ```
ibmcloud login
  ```
  {: codeblock}

  Se hai un ID utente federato, usa invece il seguente comando per eseguire l'accesso con il tuo ID SSO (single sign-on). Consulta [Accesso con un ID federato](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) per ulteriori informazioni.

  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Quindi, indica come destinazione un'organizzazione e uno spazio Cloud Foundry:
  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Se non hai un'organizzazione o uno spazio configurati, consulta [Aggiunta di organizzazioni e spazi](https://console.bluemix.net/docs/account/orgs_spaces.html).
  {: tip}

1. Dall'interno della directory *get-started-tomcat*, esegui il push della tua applicazione a {{site.data.keyword.Bluemix_notm}}
  ```
ibmcloud cf push
  ```
  {: codeblock}

  Ci possono volere circa due minuti. Se si verifica un errore nel processo di distribuzione, puoi utilizzare il comando `ibmcloud cf logs.<Your-App-Name> --recent` per risolverlo.

Quando la distribuzione è stata completata dovresti visualizzare un messaggio che indica che la tua applicazione è in esecuzione.  Visualizza la tua applicazione all'URL elencato nell'output del comando trasmesso.  Puoi anche immettere il seguente comando per visualizzare lo stato delle tue applicazioni e vedere l'URL.
  ```
ibmcloud cf apps
  ```
  {: codeblock}


## Passo 5: Aggiungi un database
{: #add_database}

Successivamente, aggiungeremo un database {{site.data.keyword.cloudant_short_notm}} a questa applicazione e la configureremo in modo che possa essere eseguita localmente e su {{site.data.keyword.Bluemix_short}}.

1. Nel tuo browser, accedi a {{site.data.keyword.Bluemix_short}} e passa al dashboard. Seleziona **Crea risorsa**.
2. Scegli la sezione **Data and Analytics** e seleziona **{{site.data.keyword.cloudant_short_notm}}** e crea il tuo servizio.
3. Passa alla vista **Connessioni** e seleziona la tua applicazione, quindi **Crea connessione**.
4. Seleziona **Riprepara** quando richiesto. {{site.data.keyword.Bluemix_short}} riavvierà la tua applicazione e fornirà le credenziali del database alla tua applicazione utilizzando la variabile di ambiente `VCAP_SERVICES`. Questa variabile di ambiente è disponibile per l'applicazione solo quando è in esecuzione su {{site.data.keyword.Bluemix_short}}.

Le variabili di ambiente ti abilitano a separare le impostazioni di distribuzione dal tuo codice di origine. Ad esempio, invece di impostare come hardcoded una password del database, puoi archiviarla in una variabile di ambiente di riferimento nel tuo codice di origine.
{: tip}

## Passo 6: Utilizza il database
{: #use_database}

Ora aggiorneremo il tuo codice locale per puntare a questo database. Archivieremo le credenziali per i servizi in un file properties. Questo file sarà utilizzato SOLO quando l'applicazione è in esecuzione localmente. Quando è in esecuzione in {{site.data.keyword.Bluemix_notm}}, le credenziali saranno lette dalla variabile di ambiente `VCAP_SERVICES`.

1. Nel tuo browser, vai al dashboard {{site.data.keyword.Bluemix_notm}} e seleziona **_la_tua_applicazione_ > Connessioni**. Fai clic sull'icona del menu {{site.data.keyword.cloudant_short_notm}} (**&vellip;**) e seleziona **Visualizza credenziali**.

2. Copia e incolla solo l'`url` dalle credenziali nel campo `url` del file `cloudant.properties` e salva le modifiche.
  ```
cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:codeblock}

3. Riavvia il server

Aggiorna la tua vista del browser all'indirizzo: http://localhost:8080/GetStartedTomcat/. Tutti i nomi immessi nell'applicazione saranno ora aggiunti al database.

  La tua applicazione locale e {{site.data.keyword.Bluemix_notm}} stanno condividendo il database. I nomi che aggiungi dall'applicazione saranno visualizzati entrambi quando aggiorni i browser.


Ricorda, se non hai bisogno della tua applicazione live su {{site.data.keyword.Bluemix_notm}}, arrestala così da non incorrere in alcun addebito non previsto.
{: tip}  

## Passi successivi

* [Esercitazioni](/docs/tutorials/index.html)
* [Esempi ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
