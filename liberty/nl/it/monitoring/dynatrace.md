---

copyright:
  years: 2016, 2018
lastupdated: "2018-06-27"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilizza Dynatrace per monitorare Liberty in {{site.data.keyword.cloud_notm}}
{: #using_dynatrace}

Dynatrace è un servizio di terze parti che fornisce monitoraggio per la tua applicazione. Puoi integrare Dynatrace con la tua applicazione Liberty, ma IBM non fornisce supporto per i servizi di terze parti. Per ulteriori informazioni, consulta [Servizi di terze parti](/docs/runtimes-common/buildpackSupport.html#third-party).

Per ulteriori informazioni su Dynatrace e la relativa licenza, consulta [Dynatrace Application Monitoring ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://www.dynatrace.com/en/products/application-monitoring.html).

Quando la tua applicazione Liberty è configurata per utilizzare Dynatrace, la modalità di funzionamento predefinita
prevede che il runtime Liberty acquisirà un file `.jar` dell'agent Dynatrace da un sito Dynatrace ed eseguirà tale agent
Dynatrace con la tua applicazione.  Con tale funzionamento predefinito la configurazione minima necessaria per utilizzare
Dynatrace è di creare un servizio fornito dall'utente che punti al tuo raccoglitore
Dynatrace.

## Creazione di un servizio fornito dall'utente che punta al raccoglitore Dynatrace

Per prima cosa, avrai bisogno di configurare un raccoglitore Dynatrace.  Quindi devi
creare un servizio fornito dall'utente per trasmettere le informazioni per l'agent Dynatrace per stabilire una connessione con il raccoglitore Dynatrace. Consulta [Dynatrace Architecture ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://community.dynatrace.com/community/display/DOCDT65/Architecture) per comprendere meglio la relazione tra i componenti Dynatrace.

1. Configura un raccoglitore Dynatrace.
  * Consulta il [sito web della community Dynatrace ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace) per istruzioni sul download e la configurazione del raccoglitore Dynatrace.
  * Verifica che il raccoglitore sia configurato in un'ubicazione che sia accessibile dall'agent Dynatrace in esecuzione con la tua applicazione in {{site.data.keyword.Bluemix_notm}}.
2. Crea un servizio fornito dall'utente che punta al raccoglitore Dynatrace in esecuzione.

  **Nota:** il nome del servizio fornito dall'utente deve contenere la stringa **dynatrace**. L'utilizzo di maiuscole/minuscole viene ignorato. Ad esempio, utilizza il seguente comando, dove **my-dynatrace-collector** contiene **dynatrace**:
  ```
  ibmcloud cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
  ```
  {: codeblock}

    In questo esempio, my-dynatrace-collector è il nome fornito al servizio, DynatraceCollectorIPaddress è l'indirizzo IP del raccoglitore Dynatrace che hai configurato e profile è il nome del profilo Dynatrace facoltativo associato a questa applicazione monitorata. Il valore predefinito è Monitoring. Puoi specificare i parametri facoltativi come nel seguente esempio.

    ```
    ibmcloud cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                      "options" : {"dynatrace-parameter-1": "value",
                                   "dynatrace-parameter-2": "value"}}'
    ```
    {: codeblock}

    Consulta la sezione [_Agent Settings_ di Agent Configuration ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://community.dynatrace.com/community/display/DOCDT65/Set+up+Agents) sul sito web della community Dynatrace per ulteriori informazioni sulle opzioni disponibili. Ad esempio, utilizzando l'opzione exclude, puoi escludere le classi dal monitoraggio di Dynatrace. Consulta [Dynatrace Agent Framework ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md) per ulteriori dettagli sulla configurazione del servizio fornito dall'utente.

3. Dopo che hai eseguito il push della tua applicazione a {{site.data.keyword.Bluemix_notm}}, esegui il bind del servizio fornito dall'utente che hai creato per l'applicazione. Ad esempio, utilizza il seguente comando:
  ```
  ibmcloud cf bs myApp my-dynatrace-collector
  ```
  {: codeblock}

    **Nota:** devi ripreparare la tua applicazione dopo il bind del servizio.

## Configurazione facoltativa
{: #optional_configuration}

Puoi scegliere di acquisire e ospitare il file `.jar` dell'agent Dynatrace tu stesso.  In questo caso sono necessari
i seguenti passi di configurazione addizionali.
1. Acquisisci e ospita il file `.jar` dell'agent Dynatrace in modo che il pacchetto di build di Liberty possa scaricarlo.
2. Configura la tua applicazione Liberty in modo che possa scaricare l'agent Dynatrace.

### Ospitare l'agent Dynatrace
{: #hosting_dynatrace_agent}
L'agent Dynatrace deve essere ospitato su un server Web e il pacchetto di build Liberty deve essere in grado di scaricare il file `.jar` dell'agent da tale server. Il server deve essere configurato con un file `index.yml` che specifica i dettagli sul `.jar` dell'agent. Completa i seguenti passi per impostare l'agent Dynatrace:
  1. Scarica il file `.jar` dell'agent Dynatrace. Consulta [Dynatrace Server Platform Installers ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace) sul sito web della community Dynatrace per istruzioni sul download del file `.jar` dell'agent Dynatrace. Il file `.jar` dell'agent appropriato per l'esecuzione su {{site.data.keyword.Bluemix_notm}} è **dynatrace-agent-unix.jar** versione **6.+**.
  2. Ospita il file `.jar` dell'agent in un'ubicazione da cui il pacchetto di build Liberty può scaricarlo. Puoi ospitarlo in {{site.data.keyword.Bluemix_notm}} stesso utilizzando una qualunque delle funzioni del server disponibili, oppure puoi ospitarlo in alcune ubicazioni disponibili pubblicamente.
     * Assicurati di fornire un file `index.yml` all'ubicazione che lo ospita. Il file `index.yml` deve contenere una voce composta dall'ID versione del file `.jar` dell'agent seguito da due punti e l'URL completo dell'ubicazione di tale file `.jar` dell'agent. Ad esempio:

            ---
               6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
            {: codeblock}

     * Il file **dynatrace-agent-6.3.0-unix.jar** deve essere disponibile nell'ubicazione specificata nel file `index.yml`. L'ubicazione sia per il file `.jar` che per `index.yml` può essere la stessa directory.

### Configurazione dell'applicazione Liberty
{: #configuring_liberty_app}

L'applicazione Liberty che desideri monitorare deve essere configurata per individuare il server che ospita il file `.jar` dell'agent che hai precedentemente configurato. Puoi configurare l'applicazione con la variabile di ambiente **JBP_CONFIG_DYNATRACEAPPMONAGENT**. La variabile di ambiente **JBP_CONFIG_DYNATRACEAPPMONAGENT** indica che il pacchetto di build da cui scaricare l'agent Dynatrace. Per impostare la variabile di ambiente, completa la seguente procedura:

1. Imposta la variabile **JBP_CONFIG_DYNATRACEAPPMONAGENT** in modo che abbia il valore *"repository_root: URL_of_server_hosting_index.yml"*. Ad esempio, dopo aver eseguito il push della tua applicazione immetti il seguente comando:

        ibmcloud cf se myApp JBP_CONFIG_DYNATRACEAPPMONAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
        {: codeblock}

    In questo esempio, *my-dynatrace-agent-host.mybluemix.net* è l'URL del file `index.yml` ospitato dal server che hai precedentemente configurato.

2. Dopo aver impostato la variabile di ambiente, riprepara la tua applicazione. Controlla il log della fase di preparazione per un messaggio che indica che hai scaricato con successo l'agent Dynatrace dal tuo server che ospita l'agent. Ad esempio:
```
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
```
{: codeblock}
