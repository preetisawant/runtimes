---

copyright:
  years: 2015, 2018
lastupdated: "2018-1-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Configura la registrazione e la traccia
{: #logging_tracing}

## File di log
{: #log_files}

I log Liberty standard, come `messages.log` o la directory `ffdc`, sono disponibili in {{site.data.keyword.Bluemix}} nella directory `logs` di ciascuna istanza dell'applicazione. A questi log è possibile accedere dalla console {{site.data.keyword.Bluemix_notm}} oppure con la CLI Cloud Foundry. Ad esempio:

* Per accedere ai log recenti di un'applicazione, esegui il seguente comando:

  ```
  cf logs --recent <appname>
  ```
  {: codeblock}


* Per visualizzare il file `messages.log` di un'applicazione, esegui il seguente comando:

  ```
  cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

Il livello di log
e le altre opzioni di traccia possono essere impostati mediante il file di configurazione di Liberty. Per ulteriori informazioni, consulta [Troubleshooting Liberty: Logging and Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html).

## Utilizzo delle funzionalità di traccia e di dump
{: #using_trace_and_dump}

### Utilizzo della traccia e del dump nella console {{site.data.keyword.Bluemix_notm}} (obsoleto)

La configurazione della traccia Liberty può essere modificata per un'applicazione in esecuzione direttamente dalla console {{site.data.keyword.Bluemix_notm}}. La console fornisce inoltre la capacità di richiedere e scaricare dump di heap e di thread. Per modificare la configurazione della traccia o per richiedere un dump, seleziona un'applicazione Liberty nella console {{site.data.keyword.Bluemix_notm}} e scegli il menu `Runtime` nella navigazione. Nella vista `Runtime`, seleziona un'istanza e premi il pulsante *TRACE* o *DUMP*. Se stai modificando il livello di traccia, consulta [Troubleshooting Liberty: Logging and Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html) per i dettagli della sintassi della specifica della traccia.

### Modifica della configurazione della traccia tramite SSH 

Quando esegui il push dell'applicazione, il file server.xml include le proprietà predefinite **updateTrigger** impostata su **polled** e **monitorInterval** impostata su 1 minuto. Il server Liberty viene automaticamente configurato per controllare gli aggiornamenti del file server.xml ogni minuto.

Consulta [Push delle applicazioni Liberty con server.xml](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing) per le opzioni per eseguire il push delle applicazioni Liberty con un sever.xml personalizzato

Consulta [Controlling Dynamic Updates](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window} per informazioni su come configurare l'aggiornamento dinamico in server.xml.

Segui questa procedura per modificare la configurazione della traccia: 

1. SSH alla tua app

  ```
 cf ssh <appname> [-i instance_index]
  ```
  {: codeblock}

2. Modifica ```<logging traceSpecification="xxxx"/>``` in server.xml per configurare la tua specifica della traccia desiderata, ad esempio utilizzando *vi*:

  ```
vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: codeblock}

Nota: la modifica a server.xml andrà persa al riavvio e alla ripreparazione ed è valida solo per l'istanza in cui esegui ssh.

Consulta [Troubleshooting Liberty: Logging and Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window} per i dettagli della sintassi della specifica della traccia.

### Attivazione dei dump tramite SSH 

Utilizza il seguente comando per attivare un dump di heap e di thread tramite la CLI CF utilizzando la funzione SSH: 

  ```
 cf ssh <appname> -c "pkill -3 java"
  ```
  {: codeblock}

Consulta la seguente documentazione per i dettagli sullo scaricamento dei file di dump generati.

## Scarica file dump
{: #download_dumps}

Per impostazione predefinita, i vari file di dump sono ubicati nella directory `dumps` del contenitore dell'applicazione. Utilizza la CLI Cloud Foundry `cf ssh` per visualizzare e scaricare i file di dump.

* Per visualizzare i dump generati, esegui il seguente comando:

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Per scaricare un file di dump, esegui il seguente comando:

  ```
  cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

È anche possibile utilizzare `scp` e altri strumenti simili per visualizzare e scaricare i file di dump. Fai riferimento a [Accessing Apps with SSH  ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) per ulteriori informazioni.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Runtime Liberty](index.html)
* [Liberty Overview](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
