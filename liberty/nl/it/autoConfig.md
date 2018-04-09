---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Configura i servizi associati
{: #auto_config}

Puoi eseguire il bind di diversi servizi alla tua applicazione Liberty for Java. I servizi possono essere gestiti dal contenitore, gestiti dall'applicazione o entrambe le cose, a seconda delle scelte
dello sviluppatore.

Un servizio gestito dall'applicazione è un servizio gestito interamente dall'applicazione,
senza alcuna assistenza da Liberty. L'applicazione di norma legge
VCAP_SERVICES per ottenere informazioni sul servizio di cui è stato eseguito il bind ed accede al servizio
direttamente. L'applicazione fornisce tutto il codice di accesso client necessario. Non c'è alcuna dipendenza dalle funzioni Liberty o dalla configurazione del file server.xml. La configurazione automatica del pacchetto di build Liberty non si applica ai servizi di
questo tipo.

Un servizio gestito dal contenitore è un servizio gestito dal runtime Liberty. In alcuni casi, l'applicazione può cercare il servizio di cui è stato eseguito il bind in JNDI, mentre in altri casi il servizio viene utilizzato direttamente da Liberty stesso. Il pacchetto di build Liberty legge VCAP_SERVICES per ottenere
informazioni sui servizi di cui è stato eseguito il bind. Per ogni servizio gestito dal contenitore, il pacchetto di build esegue tre funzioni.

* Genera le [variabili cloud](optionsForPushing.html#accessing_info_of_bound_services) per il servizio di cui è stato eseguito il bind.
* Installa le funzioni Liberty e i codici di accesso client richiesti per accedere al servizio di cui è stato eseguito il bind.
* Genera o aggiorna le stanze del file server.xml richieste dal servizio.

Questo processo viene indicato come configurazione automatica,

Il pacchetto di build Liberty fornisce la configurazione automatica per i seguenti tipi di servizio:

* [ Auto-Scaling](/docs/services/Auto-Scaling/index.html#autoscaling)
* [ClearDB MySQL Database ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.cleardb.com/developers)
* [Cloudant NoSQL Database](/docs/services/Cloudant/index.html#Cloudant)
* [Compose for MongoDB](/docs/services/ComposeForMongoDB/index.html)
* [Compose for MySQL](/docs/services/ComposeForMySQL/index.html)
* [Compose for PostgreSQL](/docs/services/ComposeForPostgreSQL/index.html)
* [dashDB](/docs/services/dashDB/index.html#dashDB)
* [ElephantSQL](docs/services/ElephantSQL/index.html)
* [Single Sign On](/docs/services/SingleSignOn/index.html#sso_gettingstarted)

I servizi Compose possono essere contenitori o applicazioni gestiti. Per impostazione predefinita,
il pacchetto di build Liberty presume che questi servizi siano gestiti dal contenitore e li configura
automaticamente. Se desideri che sia l'applicazione a gestire il servizio, puoi optare per l'esclusione della
configurazione automatica per il servizio impostando la variabile di ambiente `services_autoconfig_excludes`. Per ulteriori informazioni, consulta [Opzione di esclusione dalla configurazione automatica del servizio](autoConfig.html#opting_out).

## Installazione delle funzioni Liberty e
codice di accesso client
{: #installation_of_liberty_features}

Quando esegui il bind a un servizio gestito dal contenitore, il servizio potrebbe richiedere che le funzioni Liberty siano configurate nella stanza featureManager nel file server.xml. Il pacchetto di build
Liberty aggiorna la stanza featureManager e installa i file binari di supporto richiesti. Se il servizio richiede i jar di driver client, essi vengono scaricati in un'ubicazione nota
nell'installazione di Liberty.

Consulta la sezione [Opzione di esclusione dalla configurazione automatica del servizio](#opting_out) per ulteriori dettagli sui tipi di servizio associati.

## Generazione o aggiornamento delle stanze di configurazione di server.xml
{: #generating_or_updating_serverxml}

Il pacchetto di build Liberty può generare o aggiornare automaticamente le stanze di configurazione nel tuo file server.xml quando esegui il push di un'applicazione autonoma, a seconda di come la tua applicazione è associata ai servizi e se hai un file server.xml esistente.

Quando esegui il push di un'applicazione autonoma, il pacchetto di build Liberty genera la stanza di configurazione come descritto in [Opzioni per eseguire il push delle applicazioni Liberty](optionsForPushing.html#options_for_pushing) a {{site.data.keyword.Bluemix_notm}}.

Quando esegui il push di un'applicazione autonoma ed esegui il bind ai servizi gestiti dal contenitore, il pacchetto di build Liberty genera le stanze di server.xml necessarie per i servizi di cui è stato eseguito il bind.

Quando fornisci un file server.xml ed esegui il bind ai servizi gestiti dal contenitore, il pacchetto di build Liberty genera o aggiorna le stanze di configurazione. 

* Se il file server.xml fornito non contiene le stanze di configurazione per i servizi di cui è stato eseguito il bind, Liberty genera la configurazione per questi servizi.
* Se il file server.xml fornito contiene le stanze di configurazione per i servizi di cui è stato eseguito il bind, Liberty aggiorna la configurazione per questi servizi.

Per ulteriori dettagli, consulta la documentazione per
il tipo di servizio di cui è stato eseguito il bind.

## Opzione di esclusione dalla configurazione automatica del servizio
{: #opting_out}

In
alcuni casi, potresti non desiderare che il pacchetto di build Liberty configuri automaticamente
i servizi di cui è stato eseguito il bind. Valuta i seguenti scenari.

* La mia applicazione utilizza *dashDB*, ma io desidero che l'applicazione gestisca
direttamente la connessione al database. L'applicazione contiene il jar di
driver client necessario. Non desidero che il pacchetto di build Liberty configuri
automaticamente il servizio *dashDB*.
* Sto fornendo un file server.xml e ho fornito le stanze di configurazione per l'istanza *cloudant* perché richiedo una configurazione dell'origine dati non standard. Non desidero che il pacchetto di build Liberty aggiorni il mio file server.xml ma richiedo comunque che il pacchetto di build Liberty verifichi che sia installato il software di supporto appropriato.

Per optare per l'esclusione dalla configurazione automatica
del servizio, utilizza la variabile di ambiente services_autoconfig_excludes. Puoi includere questa variabile
di ambiente in un manifest.yml o impostarla utilizzando il client cf.

Puoi optare
per l'esclusione dalla configurazione automatica dei servizi in base ai singoli tipi di servizio. Puoi scegliere di optare per l'esclusione in modo totale (come nello scenario *dashDB*) oppure di optare per l'esclusione solo dagli aggiornamenti della configurazione del file server.xml (come nello scenario *cloudant*). Il valore da te specificato per la variabile di ambiente services_autoconfig_excludes è una stringa, come mostrato di seguito. 

* La stringa può contenere le specifiche di opzione di esclusione per uno o più servizi. 
* La specifica dell'opzione di esclusione per un servizio specifico è service_type=option, dove:
  * service_type è l'etichetta per il servizio come visualizzata in VCAP_SERVICES.
  * L'opzione è all o config.
* Se la stringa contiene una specifica di opzione di esclusione per più di un servizio,
le singole specifiche di opzione di esclusione devono essere separate da un singolo carattere spazio vuoto.

Vedi il seguente esempio di grammatica della stringa services_autoconfig_excludes: 

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: il tipo di servizio (etichetta del servizio come si presenta in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: codeblock}

**Importante**: il tipo di servizio da te specificato deve corrispondere all'etichetta services come si presenta nella variabile di ambiente VCAP_SERVICES. Lo spazio vuoto non è consentito.
**Importante**: non è consentito alcuno spazio vuoto in una ```<specifica_tipo_di_servizio>```. Il solo
utilizzo consentito dello spazio vuoto è per separare più istanze ```<specifica_di_tipo_servizio>```. 

Utilizza l'opzione **all** per optare per l'esclusione da tutte le azioni di configurazione automatica per un servizio, come nello scenario *dashDB* sopra riportato. Utilizza l'opzione **config** per optare per l'esclusione solo dalle azioni di aggiornamento della configurazione come nello scenario *cloudant* sopra riportato.

Di seguito sono riportate delle specifiche di opzione di esclusione di esempio in un file manifest.yml per gli scenari *dashDB* e *cloudant*.

```
    env:
      services_autoconfig_excludes: dashDB=all

    env:
      services_autoconfig_excludes: cloudant=config

    env:
      services_autoconfig_excludes: cloudant=config dashDB=all
```
{: codeblock}

Sono qui di seguito
riportati degli esempi di come impostare la variabile di ambiente services_autoconfig_excludes per l'applicazione
myapp utilizzando l'interfaccia riga di comando.

```
    cf set-env myapp services_autoconfig_excludes cloudant=config
    cf set-env myapp services_autoconfig_excludes "cloudant=config dashDB=all"
```
{: codeblock}

Per trovare il *label* per un servizio in VCAP_SERVICES immetti un comando simile al seguente esempio: 

```
    cf env myapp
```
{: codeblock}

L'output include un testo simile al seguente, dove puoi vedere il campo **label** con il valore **elephantsql**:

```
   "elephantsql": [
   {
      "credentials": {
      "max_conns": "5",
      "uri":      "..."
   },
   "label": "elephantsql",

```
{: codeblock}

## Sovrascrittura configurazione del servizio
{: #override_service_config}

In alcuni casi potresti voler sovrascrivere la configurazione predefinita per un servizio generato dalla configurazione automatica.
Puoi utilizzare la variabile di ambiente **LBP_SERVICE_CONFIG_xxxx** per sovrascrivere una configurazione del servizio. Consulta le seguenti tabelle per  i nomi della variabile di ambiente completi e per la sintassi di esempio per sovrascriverli.  Ad esempio, per sovrascrivere la versione predefinita del servizio *elephantSQL* ed impostare la versione 8.3.4.+ immetti un comando simile a:

```
    cf set-env myapp LBP_SERVICE_CONFIG_POSTGRESQL "{driver: { version: 8.3.4.+ }}"
```
{: codeblock}

Questa tabella mostra l'associazione dei nomi della variabile di ambiente **service_type** a **LBP_SERVICE_CONFIG_xxxx**.

<table>
<tr>
<th align="left">service_type</th>
<th align="left">Nome variabile di ambiente</th>
</tr>

<tr>
<td>Auto-Scaling</td>
<td>LBP_SERVICE_CONFIG_AUTO-SCALING</td>
</tr>

<tr>
<td>cleardb</td>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
</tr>

<tr>
<td>cloudantNoSQLDB</td>
<td>LBP_SERVICE_CONFIG_CLOUDANTNOSQLDB</td>
</tr>

<tr>
<td>compose-for-mongodb</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MONGO</td>
</tr>

<tr>
<td>compose-for-mysql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
</tr>

<tr>
<td>compose-for-postgresql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
</tr>

<tr>
<td>elephantsql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
</tr>

<tr>
<td>SingleSignOn</td>
<td>LBP_SERVICE_CONFIG_SINGLESIGNON</td>
</tr>
</table>


La seguente tabella mostra la sintassi per la sovrascrittura di alcune opzioni di configurazione del servizio:

<table>
<tr>
<th align="left">Nome variabile di ambiente</th>
<th align="left">Sintassi di configurazione</th>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>
</table>



# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
