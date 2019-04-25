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

# Sviluppa le applicazioni Tomcat con IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}

Puoi anche utilizzare {{site.data.keyword.eclipsetoolsfull}} come un modo alternativo per sviluppare e distribuire applicazioni a {{site.data.keyword.Bluemix}}. IBM Eclipse Tools fornisce plugin che è possibile installare in un ambiente Eclipse esistente per assisterti nell'integrazione del tuo IDE (integrated development environment) con {{site.data.keyword.Bluemix_notm}}.

Questa procedura segue la stessa procedura generale di [Esercitazione introduttiva](getting-started.html) per Liberty. Utilizzando Eclipse, configurerai un ambiente di sviluppo, distribuirai un'applicazione localmente e nel cloud e integrerai un servizio database nella tua applicazione.

## Prima di cominciare
{: #prereqs}

Ti serviranno i seguenti account e strumenti:
* [IBM Eclipse Tools for IBM Cloud ![External Link icon](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}
* [Eclipse IDE for Java EE Developers ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}

Se hai completato l'[Esercitazione introduttiva](getting-started.md), potresti già avere questi strumenti e account. Assicurati che anche quanto segue sia installato e registrato prima di iniziare:
* [Account {{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/registration)
* [CLI {{site.data.keyword.Bluemix_notm}}](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://git-scm.com/downloads){: new_window}
* [Maven ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat version 8.0.41 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}

## Passo 1: Clona l'applicazione di esempio
{: #clone}

Per prima cosa, clona il repository GitHub dell'applicazione di esempio.

  ```
git clone https://github.com/IBM-Cloud/get-started-tomcat
  ```
  {: codeblock}

## Passo 2: Crea il codice di origine della tua applicazione
{: #build_app}

Utilizza Maven per creare il tuo codice di origine ed eseguire l'applicazione risultante.

1. Nella riga di comando, modifica la directory in cui è ubicata l'applicazione di esempio.

  ```
cd get-started-tomcat
  ```
  {: codeblock}

1. Utilizza Maven per installare le dipendenze e creare il file .war.

  ```
mvn clean install
  ```
  {: codeblock}

## Passo 3: Prepara l'applicazione per la distribuzione
{: #prepare}

Per distribuire a {{site.data.keyword.Bluemix_notm}}, può essere utile impostare un file manifest.yml. Il manifest.yml include le informazioni di base sulla tua applicazione, come il nome, quanta memoria allocare per ogni istanza e la rotta. Abbiamo fornito un file manifest.yml di esempio nella directory `get-started-java`.

Apri il file manifest.yml e modifica `name` da `GetStartedJava` con il nome della tua applicazione, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
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

In questo file manifest.yml, **random-route: true** genera una rotta casuale per la tua applicazione per evitare il conflitto con altre rotte.  Se scegli di farlo, puoi sostituire **random-route: true** con **host: myChosenHostName**, fornendo un nome host di tua scelta.
{: tip}

## Passo 4: Esegui l'accesso a {{site.data.keyword.Bluemix_notm}}
{: #deploy}

1. Esegui l'accesso al tuo account {{site.data.keyword.Bluemix_notm}} e seleziona un endpoint API.
  ```
ibmcloud login
  ```
  {: codeblock}

  Se non puoi eseguire l'accesso utilizzando `ibmcloud login` perché hai un ID utente federato, utilizza quanto segue per eseguire l'accesso con il tuo ID SSO (single sign-on). Consulta [Accesso con un ID federato](https://cloud.ibm.com/docs/iam?topic=iam-federated_id#federated_id) per ulteriori informazioni.
  ```
ibmcloud login --sso
  ```
  {: codeblock}

  Quindi, indica come destinazione la CLI Cloud Foundry:
  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Se non hai un'organizzazione o uno spazio configurati, consulta [Aggiunta di organizzazioni e spazi](https://cloud.ibm.com/docs/account?topic=account-orgsspacesusers#orgsspacesusers).
  {: tip}

## Passo 5: Sviluppa utilizzando Eclipse
{: #eclipse}

1. Assicurati di disporre di [IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix).

2. Importa l'esempio `get-started-java` in Eclipse da **File > Import > Maven > Existing Maven Projects**.

3. Crea una definizione server Tomcat:
  - Nella vista **Servers**, fai clic con il tasto destro del mouse e seleziona **New > Server**.
  - Seleziona **Apache > Tomcat v8.0 Server**.
  - Scegli la tua `tomcat-install-dir`.
  - Continua la procedura guidata con le opzioni predefinite per finire.

4. Esegui la tua applicazione localmente sul server Apache:
  - Fai clic con il tasto destro del mouse sull'esempio `GetStartedTomcat` e seleziona **Run As > Run on Server**.
  - Trova e seleziona il server Tomcat localhost e fai clic su **Finish**.
  - In pochi secondi, la tua applicazione dovrebbe essere eseguita all'indirizzo http://localhost:8080/GetStartedTomcat/

5. Esegui la tua applicazione su {{site.data.keyword.Bluemix_notm}}:
  - Fai clic con il tasto destro sull'esempio `GetStartedTomcat` e seleziona **Run As > Run on Server**.
  - Trova e seleziona **{{site.data.keyword.Bluemix_notm}}** e fai quindi clic su **Finish**.
  - Una procedura guidata ti guiderà con le opzioni di distribuzione. Assicurati di scegliere un `Name` univoco per la tua applicazione.
  - In pochi minuti, la tua applicazione sarà in esecuzione all'URL che hai scelto.

Ora stai eseguendo il tuo codice sia localmente che sul cloud!

## Passo 6: Aggiungi un database
{: #add_database}

Successivamente, aggiungeremo un database {{site.data.keyword.cloudantfull}} a questa applicazione e la configureremo in modo che possa essere eseguita localmente e su {{site.data.keyword.Bluemix_notm}}.

1. Nel tuo browser, accedi a {{site.data.keyword.Bluemix_notm}} e passa al dashboard. Seleziona **Crea risorsa**.
2. Scegli la sezione **Data and Analytics** e seleziona **{{site.data.keyword.cloudant_short_notm}}** e crea il tuo servizio.
3. Passa alla vista **Connessioni** e seleziona la tua applicazione, quindi **Crea connessione**.
4. Seleziona **Riprepara** quando richiesto. {{site.data.keyword.Bluemix_notm}} riavvierà la tua applicazione e fornirà le credenziali del database alla tua applicazione utilizzando la variabile di ambiente `VCAP_SERVICES`. Questa variabile di ambiente è disponibile per l'applicazione solo quando è in esecuzione su {{site.data.keyword.Bluemix_notm}}.

Le variabili di ambiente ti abilitano a separare le impostazioni di distribuzione dal tuo codice di origine. Ad esempio, invece di impostare come hardcoded una password del database, puoi archiviarla in una variabile di ambiente di riferimento nel tuo codice di origine.
{: tip}

## Passo 7: Utilizza il database
{: #use_database}
Ora aggiorneremo il tuo codice locale per puntare a questo database. Archivieremo le credenziali per i servizi in un file properties. Questo file sarà utilizzato SOLO quando l'applicazione è in esecuzione localmente. Quando è in esecuzione in {{site.data.keyword.Bluemix_notm}}, le credenziali saranno lette dalla variabile di ambiente VCAP_SERVICES.

1. Apri Eclipse e il file src/main/resources/cloudant.properties:

  ```
  cloudant_url=
  ```
  {: codeblock}

2. Nel tuo browser apri la IU {{site.data.keyword.Bluemix_notm}}, seleziona la tua Applicazione -> Connessioni -> Cloudant -> Visualizza credenziali

3. Copia e incolla solo l'`url` dalle credenziali nel campo `url` del file `cloudant.properties` e salva le modifiche.  Il risultato sarà qualcosa di simile:

  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {: codeblock}

4. Riavvia il server Liberty in Tomcat dalla vista `Servers`.

  Aggiorna la tua vista del browser all'indirizzo: http://localhost:8080/GetStartedTomcat/. Tutti i nomi immessi nell'applicazione saranno ora aggiunti al database.

  La tua applicazione locale e {{site.data.keyword.Bluemix_notm}} stanno condividendo il database.  Visualizza la tua applicazione {{site.data.keyword.Bluemix_notm}} all'URL elencato nell'output del comando trasmesso precedentemente.  I nomi che aggiungi dall'applicazione dovrebbero essere visualizzati entrambi quando aggiorni i browser.

Ricorda: se non hai bisogno della tua applicazione live su {{site.data.keyword.Bluemix_notm}}, arrestala così da non incorrere in alcun addebito non previsto.
{: tip}
