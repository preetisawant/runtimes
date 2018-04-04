---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilizza le funzioni beta
{: #using_beta_features}

Le funzioni beta Liberty forniscono un accesso anticipato ai nuovi modelli di funzionalità e
programmazione che potrebbero essere inclusi in una futura release di Liberty. La maggior parte delle funzioni beta può essere
utilizzata anche nelle applicazioni distribuite a {{site.data.keyword.Bluemix}}.

**Importante**: le funzioni beta sono solo per scopi di sviluppo e test e non possono essere utilizzate in produzione. Per le condizioni di utilizzo complete, consulta l'[ accordo di licenza beta](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

Funzioni beta Liberty disponibili in {{site.data.keyword.Bluemix_notm}}
<table>
<tr>
<th align="left">Funzioni </th>
</tr>

<tr>
    <tr><td>appSecurity-3.0</tr></td>
    <tr><td>audit-1.0</tr></td>
    <tr><td>beanValidation-2.0</tr></td>
    <tr><td>bluemixLogCollector-1.1</tr></td>
    <tr><td>cdi-2.0</tr></td>
    <tr><td>javaee-8.0</tr></td>
    <tr><td>javaeeClient-8.0</tr></td>
    <tr><td>jaxrs-2.1</tr></td>
    <tr><td>jpa-2.2</tr></td>
    <tr><td>jpaContainer-2.2</tr></td>
    <tr><td>jsf-2.3</tr></td>
    <tr><td>jsfContainer-2.2</tr></td>
    <tr><td>jsonb-1.0</tr></td>
    <tr><td>jsonbContainer-1.0</tr></td>
    <tr><td>jsonp-1.1</tr></td>
    <tr><td>jsonpContainer-1.1</tr></td>
    <tr><td>logstashCollector-1.1</tr></td>
    <tr><td>mpConfig-1.2</tr></td>
    <tr><td>mpOpenAPI-1.0</tr></td>
    <tr><td>mpRestClient-1.0</tr></td>
    <tr><td>opentracing-1.0</tr></td>
    <tr><td>servlet-4.0</tr></td>
    <tr><td>validator-1.0</tr></td>
    <tr><td>webProfile-8.0</tr></td>

</tr>
</table>

Per utilizzare le funzioni beta Liberty in {{site.data.keyword.Bluemix_notm}} devi fare quanto segue:

1. [Distribuire una directory server o un server in pacchetto](optionsForPushing.html) con una o più funzioni beta abilitate nel file server.xml come nel seguente esempio:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>mpOpenAPI-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Imposta la variabile di ambiente **IBM_LIBERTY_BETA** su **true**. Questa variabile indica al pacchetto di build Liberty
di installare e abilitare le funzioni beta per la tua applicazione.  Ad esempio:
  * utilizzando lo strumento di riga di comando cf:
```
       $ cf set-env <nomedellatuaapplicazione> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * oppure utilizzando il file manifest.yml:
```
      env:
          IBM_LIBERTY_BETA: "true"
```

3. Imposta la variabile di ambiente **JBP_CONFIG_LIBERTY** su **"version: +"**. Questa variabile abilita il [Runtime mensile Liberty](buildpackDefaults.html#liberty_versions) il quale supporta le funzioni beta. Ad esempio:
  * utilizzando lo strumento di riga di comando cf:
```
       $ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * oppure utilizzando il file manifest.yml:
```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
```

Se stai abilitando le funzioni beta su un'applicazione esistente, non dimenticare di ripreparare la tua applicazione dopo la configurazione delle variabili di ambiente.

{: #codeblock}

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Runtime Liberty for Java](index.html)
* [Liberty Overview](https://www.ibm.com/support/knowledgecenter/SSAW57_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/cwlp_about.html)
