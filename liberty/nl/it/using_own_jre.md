---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilizza il tuo JRE
{: #using_own_jre}

Puoi eseguire la tua applicazione Liberty su {{site.data.keyword.Bluemix}} con il tuo JRE. Il pacchetto di build liberty-for-java fornirà il supporto per i [runtime supportati da WebSphere Liberty](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_restrict.html#rwlp_restrict__rest13) ma non può garantire la piena funzionalità delle versioni supportate. Devi completare le seguenti informazioni per rendere il tuo JRE disponibile per la tua applicazione.
* Ospitare il JRE in un'ubicazione da cui il pacchetto di build può scaricarlo.
* Ospitare un file `index.yml` che fornisce l'ubicazione del JRE ospitato.
* Configurare la tua applicazione per utilizzare il tuo JRE.

## Ospitare il JRE e `index.yml`
{: #hosting_jre}

Devi ospitare il file JRE su un server web da cui il pacchetto di build liberty-for-java può scaricarlo.  Puoi ospitare il file in {{site.data.keyword.Bluemix_notm}} con una qualunque delle funzioni del server disponibili, oppure puoi ospitarlo nelle ubicazioni disponibili pubblicamente. Il server deve essere configurato con un file `index.yml` che specifica i dettagli sul file JRE.

Completa i seguenti passi per ospitare JRE e il file `index.yml`:
  1. Acquisisci il JRE, che deve essere la versione per l'utilizzo su un SO a 64-bit Unix e deve essere un file `tar.gz`.
  2. Ospita il file JRE dell'agent in un'ubicazione da cui il pacchetto di build liberty-for-java può scaricarlo.
  3. Fornisci un file `index.yml` all'ubicazione che lo ospita. Il file `index.yml` deve includere una voce che contiene un ID versione del JRE seguito da due punti e l'URL completo dell'ubicazione del file JRE.
    * Definisci la versione JRE nel `index.yml`.

    ```
    ---
    jre_version: https://hostingLocation/jreName.tar.gz
    ```
    {: codeblock}

    * Includi l'ID versione del JRE e completa l'ubicazione del file JRE.  Ad esempio:

    ```
    ---
    1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```
    {: codeblock}

## Configura l'applicazione
{: #configure_app}

Devi impostare due variabili di ambiente nell'applicazione Liberty per configurare il pacchetto di build in modo che utilizzi un JRE alternativo. Configura **JBP_CONFIG_OPENJDK** per identificare l'ubicazione del file `index.yml` e imposta la variabile di ambiente **JVM** su *openjdk*. Per ulteriori informazioni sul formato delle stringhe versione-valore, consulta la documentazione Cloud Foundry in [Version Syntax and Ordering and Wildcards ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/util-repositories.md){: new_window}.

Il valore per la variabile **JBP_CONFIG_OPENJDK** è l'ubicazione del file `index.yml` e la versione JRE da scegliere dal file index.yml.

```
'{repository_root: "https://locationToIndexYml", version: version-value}'
```
{: codeblock}

Immetti il comando `ibmcloud cf se myAPP` per impostare la variabile **JBP_CONFIG_OPENJDK**, ad esempio:
```
ibmcloud cf se myApp JBP_CONFIG_OPENJDK '{repository_root: "https://myHostingApp.ng.bluemix.net", version: 1.8.+}'
```
{: codeblock}

L'URL *repository_root* non include `index.yml` nell'URL. L'URL *repository_root* punta a un livello di directory che contiene il file `index.yml`, non al file stesso.

Per impostare la variabile di ambiente JVM, immetti il seguente comando:
```
ibmcloud cf se myApp JVM 'openjdk'
```
{: codeblock}

**Nota**: riprepara la tua applicazione dopo la configurazione delle variabili di ambiente per rendere effettive le modifiche.

## Conferma
{: #confirmation}

Per confermare che Liberty utilizza il JRE previsto, controlla il log della fase di preparazione. Cerca un messaggio che indica che il server ha scaricato il pacchetto dal percorso indicato nel file `index.yml`. Vedi il seguente frammento per un esempio dell'output del log quando Liberty utilizza correttamente il JRE previsto.
```
 -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}
