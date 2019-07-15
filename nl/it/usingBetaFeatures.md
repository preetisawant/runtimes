---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-10"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilizza le funzioni beta
{: #using_beta_features}

Le funzioni beta Liberty forniscono un accesso anticipato ai nuovi modelli di funzionalità e
programmazione che potrebbero essere inclusi in una futura release di Liberty. La maggior parte delle funzioni beta può essere
utilizzata anche nelle applicazioni distribuite a {{site.data.keyword.Bluemix}}.

**Importante**: le funzioni beta sono solo per scopi di sviluppo e test e non possono essere utilizzate in produzione. Per i termini di utilizzo completi, consulta l'[accordo di licenza beta](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

| Funzioni |
| ------ |
| `audit-1.0` |
| `logstashCollector-1.1` |
| `mpConfig-1.3` |
| `mpFaultTolerance-1.1` |
| `usageMetering-1.0` |
| `validator-1.0` |
{: caption="Tabella 1. Funzioni beta Liberty disponibili in Liberty for Java in {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

Per utilizzare le funzioni beta Liberty in {{site.data.keyword.Bluemix_notm}}, dovrai eseguire quanto segue:

1. [Distribuire una directory server o un server in pacchetto](optionsForPushing.html) con una o più funzioni beta abilitate nel file server.xml come nel seguente esempio:

  ```
<server>
    <featureManager>
        <feature>usageMetering-1.0</feature>
        <feature>validator-1.0</feature>
    </featureManager>
</server>
  ```
  {: .codeblock}

2.  Imposta la variabile di ambiente `IBM_LIBERTY_BETA` su `true`. Questa variabile indica al pacchetto di build Liberty
di installare e abilitare le funzioni beta per la tua applicazione.  Ad esempio:
  * Utilizzando la CLI [{{site.data.keyword.Bluemix_notm}}](../../cli/reference/bluemix_cli/download_cli.html):
    ```
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_BETA true
    ```
    {: .codeblock}

  * Oppure utilizzando il file `manifest.yml`:
    ```
      env:
          IBM_LIBERTY_BETA: "true"
    ```
    {: .codeblock}

3. Imposta la variabile di ambiente `JBP_CONFIG_LIBERTY` su `"version: +"`. Questa variabile abilita il [Runtime mensile Liberty](buildpackDefaults.html#liberty_versions), che supporta le funzioni beta. Ad esempio:
  * Utilizzando lo strumento CLI {{site.data.keyword.Bluemix_notm}}:
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ```
    {: .codeblock}

  * Oppure utilizzando il file `manifest.yml`:
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
    ```
    {: .codeblock}

Se stai abilitando le funzioni beta su un'applicazione esistente, non dimenticarti di ripreparare la tua applicazione dopo che hai impostato le variabili di ambiente.
