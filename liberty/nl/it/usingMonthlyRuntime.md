---

copyright:
  years: 2019
lastupdated: "2019-02-01"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilizza il runtime mensile
{: #using_monthly_runtime}

Il runtime mensile Liberty fornisce la versione più recente e l'accesso ai nuovi modelli di programmazione e funzionalità.

Per utilizzare il runtime mensile Liberry in {{site.data.keyword.Bluemix_notm}}, dovrai eseguire quanto segue:

Imposta la variabile di ambiente `JBP_CONFIG_LIBERTY` su `"version: +"` e la variabile di ambiente `IBM_LIBERTY_MONTHLY` su `true`. Queste variabili abilitano il [runtime mensile Liberty](/docs/runtimes/liberty/buildpackDefaults.html#liberty_versions). Ad esempio:
  * Utilizzando lo strumento CLI {{site.data.keyword.Bluemix_notm}}:
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_MONTHLY true
    ```
    {: .codeblock}

  * Oppure utilizzando il file `manifest.yml`:
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
          IBM_LIBERTY_MONTHLY: true
    ```

    ```
      env:
          JBP_CONFIG_LIBERTY: "[version: +, app_archive: {features: [javaee-8.0]}]"
          IBM_LIBERTY_MONTHLY: true
    ```
    {: .codeblock}

Se stai abilitando il runtime mensile su un'applicazione esistente, potresti dover eliminare la tua applicazione ed eseguirne nuovamente il push dopo che hai impostato le variabili di ambiente.
