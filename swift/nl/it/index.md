---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Cloud Runtime for Swift
{: #swift_runtime}

Il Runtime per Swift su {{site.data.keyword.Bluemix}} si avvale della tecnologia del pacchetto di build [{{site.data.keyword.Bluemix_notm}} Swift](https://github.com/IBM-Swift/swift-buildpack) (ossia swift_buildpack).
Questo pacchetto di build fornisce un ambiente di runtime completo per le applicazioni Swift.
{: shortdesc}

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} fornisce un'applicazione starter [ Swift basata su Kitura ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM-Cloud/Kitura-Starter). L'applicazione starter Kitura è un'applicazione semplice Swift che puoi utilizzare per avere informazioni sui tipi di applicazioni del server che puoi distribuire utilizzando il linguaggio di programmazione Swift. Questa applicazione di esempio crea un server HTTP Kitura di base che restituisce del contenuto HTML al client.

**Nota:** l'applicazione starter di Kitura è pensata per essere utilizzata per scopi didattici. Puoi fare delle prove con l'applicazione starter facendo delle modifiche ed eseguirne il push all'ambiente {{site.data.keyword.Bluemix_notm}}. Consulta [Utilizzo di applicazioni starter](../common/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

## Ridenominazione della tua applicazione
{: #renaming_your_app}

Se desideri ridenominare la tua applicazione, dallo starter Kitura o più genericamente, sono presenti alcune modifiche che devono essere effettuate. Questo evita confusione e assicura uno sviluppo senza errori.

- Ridenomina la cartella del progetto dell'applicazione in modo che corrisponda al tuo nome dell'applicazione.
- `Package.swift` - Modifica le seguenti voci:
    - `name` - Deve corrispondere al nome dell'applicazione.
    - `targets[Target(name:)]` - Deve corrispondere al nome dell'applicazione.
- `manifest.yml` - Modifica le seguenti voci:
    - `name` - Deve corrispondere al nome dell'applicazione.
    - `command` - Il nome dell'eseguibile per avviare la tua applicazione (deve corrispondere al nome specificato nel file Package.swift).

## Versioni di runtime
{: #runtime_versions}

Il [Runtime per Swift ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM-Swift/swift-buildpack) (swift_buildpack) ospitato in {{site.data.keyword.Bluemix_notm}} è aggiornato per l'utilizzo dell'ultima versione GA dei file binari Swift. Questa è la versione consigliata di Swift da utilizzare nella tua applicazione. Il pacchetto di build elenca altre versioni Swift all'interno del suo file [manifest.yml ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml), memorizzate nella cache nel pacchetto di build per fornire un tempo di provisioning ridotto.

Se desideri utilizzare una differente versione di Swift su {{site.data.keyword.Bluemix_notm}} per la tua applicazione, puoi specificare la versione con un file `.swift-version` nella root del tuo repository. Questo file `.swift-version` definisce quale versione di Swift deve essere utilizzata dal swift_buildpack.

```
$ cat .swift-version
4.1.2
```
{: pre}

Poiché vi sono frequenti aggiornamenti nel linguaggio Swift, dovresti sempre includere un file `.swift-version` in modo che la tua applicazione sia "indicata" alla versione Swift e la tua applicazione la possa utilizzare.

Tieni presente che puoi specificare una qualsiasi versione valida di Swift nel tuo file `.swift-version`. Queste versioni alternative devono corrispondere alla denominazione di [Swift.org ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://swift.org/download/), da cui vengono scaricate direttamente. Quando si utilizza una versione senza cache il provisioning sarà un po' più lungo, non esistono differenze nelle prestazioni del runtime della tua applicazione Swift.

Il swift_buildpack predefinito in {{site.data.keyword.Bluemix_notm}} verrà utilizzato se la directory root della tua applicazione contiene un file `Package.swift`.  Se desideri utilizzare un pacchetto di build alternativo, devi specificarlo aggiungendo una voce `buildpack: {buildpackUrl}` al file manifest.yml della tua applicazione. In alternativa, puoi definirlo al momento della distribuzione, utilizzando l'argomento del comando `ibmcloud cf push -b {buildpackUrl}`.


## Ambienti dello sviluppatore

Gli sviluppatori dispongono di molte opzioni quando creano le applicazioni lato server con Swift. Chi utilizza un dispositivo macOS di Apple potrebbe preferire l'utilizzo dell'IDE Xcode, seppure non sia un requisito.  Le applicazioni basate su Swift che saranno distribuite ed eseguite su {{site.data.keyword.Bluemix_notm}} possono utilizzare qualsiasi IDE o editor di programmazione.  L'evidenziazione la pulitura della sintassi per Swift sono disponibili per molti editor comuni. Lo strumento di riga di comando Swift REPL incluso nei file binari da [Swift.org ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://swift.org/), consente la verifica e la compilazione locale prima della distribuzione a {{site.data.keyword.Bluemix_notm}}.

Per gli utenti macOS, puoi utilizzare [Kitura App ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.kitura.io/app.html) che semplifica la creazione, la distribuzione, la gestione e il controllo delle applicazioni Swift lato server in esecuzione su {{site.data.keyword.Bluemix_notm}}.  


## Integrazione avanzata

L'utilizzo dei [Framework web di Kitura](http://ibm-swift.github.io/Kitura/) fornisce molte funzionalità. Kitura è modulare per natura e vorrai presto estenderne le funzionalità con SDK compressi, per fornire funzioni come l'autenticazione, l'accesso ai servizi basati su Watson e una grande varietà di database.  Kitura fornisce il supporto per molti database direttamente, mentre altri progetti open source forniscono anche le SDK per molte piattaforme del database. Il seguente è un elenco non completo di SDK fornite da Kitura da utilizzare con le risorse esterne.

- [IBM Watson Developer Cloud Swift SDK ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/watson-developer-cloud/swift-sdk/)
- [SwiftMetrics ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/RuntimeTools/SwiftMetrics)
- [IBM Cloudant and CouchDB ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM-Swift/Kitura-CouchDB)
- [KituraKit ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM-Swift/KituraKit)
- [Swift Kuery ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/Swift-Kuery/)
- [Swift Kuery ORM ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/IBM-Swift/Swift-Kuery-ORM)

Per trovare altri pacchetti Swift da includere nella tua applicazione, vai alla sezione Packages di [Kitura.io](https://www.kitura.io/packages.html). I pacchetti possono essere aggiunti all'applicazione Swift includendo i dettagli della versione e dell'URL Git del pacchetto nel file `Package.swift` dell'applicazione. Per ulteriori dettagli sulla gestione del pacchetto, fai riferimento alla sezione [Package Manager di Swift.org](https://swift.org/package-manager/).


## Informazioni correlate

Esistono altri strumenti online disponibili da IBM per lo sviluppatore Swift.
- [IBM Swift DevCenter ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/swift/) - Sito di destinazione principale per tutte le informazioni su IBM Swift. Puoi trovare informazioni sulle nostre offerte, blog, eventi sociali, documentazione e altro.
- [Kitura.io ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.kitura.io/index.html) fornisce novità, esempi e risorse per la creazione di applicazioni Kitura.
- [Swift@IBM Slack ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://swift-at-ibm-slack.mybluemix.net/) fornisce forum per fare domande e risolvere i problemi con il team Swift@IBM.
