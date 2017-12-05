---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Configura la registrazione e la traccia 
{: #logging_tracing}

## File di log
{: #log_files}

I log Liberty standard, come `messages.log` o la directory `ffdc`, sono disponibili in IBM Bluemix nella directory `logs` di ciascuna istanza dell'applicazione. A questi log è possibile accedere dalla console IBM Bluemix oppure con la CLI CF. Ad esempio:

* Per accedere ai log recenti di un'applicazione, esegui il seguente comando:

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* Per visualizzare il file `messages.log` di un'applicazione in esecuzione su un nodo DEA, esegui il seguente comando:

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* Per visualizzare il file `messages.log` di un'applicazione in esecuzione su una cella Diego, esegui il seguente comando:

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

Il livello di log
e le altre opzioni di traccia possono essere impostati mediante il file di configurazione di Liberty. Per ulteriori informazioni, consulta [Liberty profile: Trace and logging](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html). La traccia può anche essere regolata su un'istanza dell'applicazione in esecuzione utilizzando la console IBM Bluemix.

## Utilizzo delle funzionalità di traccia e di dump
{: #using_trace_and_dump}

La configurazione della traccia Liberty può essere modificata per un'applicazione in esecuzione direttamente dalla console IBM Bluemix. La console fornisce inoltre la capacità di richiedere e scaricare dump di heap e di thread. Per modificare la configurazione della traccia o per richiedere un dump, seleziona un'applicazione Liberty nella console Bluemix e scegli il menu `Runtime` nella navigazione. Nella vista `Runtime`, seleziona un'istanza e premi il pulsante *TRACE* o *DUMP*. Se stai modificando il livello di traccia, consulta [Liberty profile: Trace and logging](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html) per i dettagli della sintassi della specifica della traccia.

### Modifica della configurazione della traccia tramite SSH in Diego

Per un'applicazione Liberty in esecuzione in una cella Diego, puoi modificare la configurazione della traccia tramite la CLI Cloud Foundy utilizzando la funzione SSH.

L'applicazione trasmessa deve includere un server.xml che contiene **updateTrigger** con il valore **polled**, quindi le modifiche alla specifica della traccia in server.xml saranno individuate e applicate all'ambiente di runtime.

Consulta [push delle applicazioni Liberty con server.xml](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing) per le opzioni per eseguire il push delle applicazioni Liberty con un sever.xml personalizzato

Consulta [Controlling Dynamic Updates![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window} per informazioni su come configurare l'aggiornamento dinamico in server.xml.

Per modificare la configurazione della traccia, completa la seguente procedura:

1. SSH alla tua app

  ```
$ cf ssh <appname> [-i instance_index]
  ```
  {: pre}

2. Modifica ```<logging traceSpecification="xxxx"/>``` in server.xml per configurare la tua specifica della traccia desiderata, ad esempio utilizzando *vi*:

  ```
$ vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: pre}

Nota: la modifica a server.xml andrà persa al riavvio e alla ripreparazione ed è valida solo per l'istanza in cui esegui ssh.

Consulta [Liberty profile: Trace and logging ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window} per i dettagli della sintassi della specifica della traccia.

### Dump di attivazione tramite SSH in Diego

Per un'applicazione in esecuzione in una cella Diego, puoi attivare un dump di heap e di thread tramite la CLI CF utilizzando la funzione SSH. Ad esempio:

  ```
$ cf ssh <appname> -c "pkill -3 java"
  ```
  {: pre}

Consulta la seguente documentazione per i dettagli sullo scaricamento dei file di dump generati.

## Scarica file dump
{: #download_dumps}

Per impostazione predefinita, i vari file di dump sono ubicati nella directory `dumps` del contenitore dell'applicazione.

### Applicazione DEA

Per un'applicazione in esecuzione in un nodo DEA, utilizza la funzionalità "cf files" per visualizzare e scaricare i file di dump.

* Per visualizzare i dump generati, esegui il seguente comando:

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* Per scaricare un file di dump, esegui i seguenti comandi:

    1. Ottieni il GUID dell'applicazione

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. Scarica il file di dump

      ```
      $ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
      ```
      {: codeblock}

### Applicazione Diego

Per un'applicazione in esecuzione in una cella Diego, utilizza la funzionalità "cf ssh" per visualizzare e scaricare i file di dump.

* Per visualizzare i dump generati, esegui il seguente comando:

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Per scaricare un file di dump, esegui il seguente comando:

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

È anche possibile utilizzare `scp` e altri strumenti simili per visualizzare e scaricare i file di dump. Fai riferimento a [Accessing Apps with SSH  ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) per ulteriori informazioni.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
