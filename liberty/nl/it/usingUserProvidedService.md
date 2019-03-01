---

copyright:
  years: 2017, 2018
lastupdated: "2018-6-26"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Utilizzo di un servizio fornito dall'utente con Liberty in {{site.data.keyword.cloud_notm}}
{: #using_user_provided}

Cloud Foundry fornisce un meccanismo per connettersi a, e utilizzare, servizi che non sono necessariamente forniti dall'ambiente {{site.data.keyword.Bluemix_notm}} o in esso disponibili.
Tale funzione consiste nei [servizi forniti dall'utente](https://docs.cloudfoundry.org/devguide/services/user-provided.html).

Questo documento presume che:
  * hai qualche servizio disponibile,
  * puoi ottenere le credenziali per tale servizio e descrive la procedura necessaria per connettersi a tale servizio e utilizzarlo con l'applicazione campione
Getting-Started-Liberty di esempio

Per questa discussione, utilizzeremo l'istanza CloudantNoSQLDB come nostro servizio di esempio e
creeremo un servizio fornito dall'utente da connettere ad esso.

## Passo 1: Esegui il push dell'applicazione Getting-Started
{: #follow_getting_started}

Attieniti alla procedura nell'[esercitazione introduttiva](/docs/runtimes/liberty/getting-started.html) fino all'esecuzione del push dell'applicazione a {{site.data.keyword.Bluemix_notm}}.  Fermati prima di connettere il database.

## Passo 2: Crea un'istanza CloudantNoSQLDB
{: #create_cloudantnosqldb}

Attieniti alla procedura nell'[esercitazione introduttiva](/docs/runtimes/liberty/getting-started.html) per creare un'istanza CloudantNoSqLDB

Utilizzare l'opzione di visualizzazione delle credenziali per copiare le credenziali dal CloudandNoSQLDB. Salva queste credenziali in un file locale, ad esempio cloudant-creds.

## Passo 3: Crea un servizio fornito dall'utente
Per lavorare con l'applicazione Getting-Started,
il nome del servizio fornito dall'utente deve contenere
"cloudantNoSQLDB".  l'applicazione Getting-Started sta analizzando la variabile dei
servizi VCAP e cercando un servizio fornito dall'utente con un nome che contiene "cloudantNoSQLDB".

        ibmcloud cf cups my-cloudantNoSQLDB-ups -p cloudant-creds

## Passo 4: Associa mediante bind il servizio fornito dall'utente e riprepara l'applicazione
Associa mediante bind il servizio fornito dall'utente all'applicazione Getting-Started.

        ibmcloud cf bs GettingStartedLiberty my-cloudantNoSQLDB-ups

        ibmcloud cf restage GettingStartedLiberty

## Passo 5: Conferma
Vai alla tua applicazione e conferma che puoi aggiungere più nomi al campo 'name'.
