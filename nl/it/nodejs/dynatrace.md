---

copyright:
  years: 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilizza Dynatrace per monitorare Node.js in {{site.data.keyword.cloud_notm}}
{: #using_dynatrace}

Dynatrace è un servizio di terze parti che fornisce monitoraggio per la tua applicazione. Puoi integrare Dynatrace con la tua applicazione Node.js, ma IBM non fornisce supporto per i servizi di terze parti. Per ulteriori informazioni, consulta [Servizi di terze parti](../common/buildpackSupport.html#third-party).

Per informazioni su Dynatrace e la relativa licenza, consulta [Dynatrace Application Monitoring ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.dynatrace.com/en/products/application-monitoring.html).

Quando la tua applicazione Node.js è configurata per utilizzare Dynatrace, il runtime Node.js acquisisce uno script di installazione Dynatrace PaaS (platform as a service) da un sito Dynatrace ed esegue tale agent Dynatrace con la tua applicazione. Per integrare Dynatrace con la tua applicazione, devi creare un servizio fornito dall'utente ed eseguire quindi il bind del servizio alla tua applicazione.

## Integrazione di Dynatrace con la tua applicazione

1. Esegui l'accesso al tuo account Dynatrace e genera un token PaaS. Per i dettagli, consulta la sezione [Generate PaaS token ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/how-do-i-monitor-cloud-foundry-applications/) nella documentazione del monitoraggio delle applicazioni Dynatrace Cloud Foundry.

  Annota i tuoi ID ambiente e token.
1. Crea un servizio fornito dall'utente che punti alle tue credenziali Dynatrace immettendo il seguente comando. Il nome del servizio deve contenere la stringa `dynatrace`, come ad esempio `dynatrace-service`.

    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken"
    ```
    {: codeblock}
    
    **Nota:** non sostituire `environmentid` o `apitoken` con le tue credenziali. Dopo aver eseguito il comando, ti verranno richiesti i loro valori.

    Se stai utilizzando Dynatrace Managed, aggiungi anche il campo `apiurl`, che specifica l'endpoint API del tuo server gestito.
    
    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken, apiurl"
    ```
    {: codeblock}
    
    Quando ti viene richiesto dopo che hai eseguito il comando, imposta `apiurl` su ` https://<YourManagedServerURL>/e/<environmentID>/api`.
    
1. Dopo che hai eseguito il push della tua applicazione a {{site.data.keyword.Bluemix_notm}}, esegui il bind del servizio fornito dall'utente che hai creato per l'applicazione. Ad esempio, utilizza il seguente comando:
    ```
    ibmcloud cf bs myApp dynatrace-service
    ```
    {: codeblock}

    **Nota**: devi ripreparare la tua applicazione dopo il bind del servizio.

   In alternativa, puoi eseguire il bind del servizio alla tua applicazione aggiungendo il nome del tuo servizio fornito dall'utente alla sezione `service` del file `manifest.yml` della tua applicazione.
   ```yaml
   ---
    applications:
    - path: .
      memory: 256M
      instances: 1
      name: myApp
      host: myApp
      disk_quota: 1024M
    services:
      - dynatrace-service
   ```
   {: codeblock}
