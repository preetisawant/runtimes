---

copyright:
  years: 2015, 2018
lastupdated: "2017-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}

Il runtime Go su {{site.data.keyword.Bluemix}} si avvale della tecnologia go_buildpack.
go_buildpack fornisce un ambiente di runtime completo per la applicazione GO.
{: shortdesc}

go_buildpack viene utilizzato se la tua applicazione contiene un file denominato *.go.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} Fornisce un'applicazione starter Go.  L'applicazione starter Go è un'applicazione Go semplice che fornisce un template che puoi utilizzare per la tua applicazione. Puoi sperimentare l'applicazione starter ed effettuare e inviare modifiche all'ambiente {{site.data.keyword.Bluemix_notm}} Consulta [Utilizzo di applicazioni starter](../common/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

## Versioni di runtime
{: #runtime_versions}

Puoi specificare la versione di Go che deve essere utilizzata dalla tua applicazione impostando la proprietà GoVersion nel file Godeps/Godeps.json a livello della root della tua applicazione. Ad esempio:

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.8.3",
	"Deps": []
}
```
{: codeblock}
Per ulteriori informazioni, consulta [godep](https://github.com/tools/godep){: new_window}.

Quando non viene specificata una versione, viene scelta per impostazione predefinita la versione 1.8.3.

### Versioni disponibili:
{: #available_versions}

Le seguenti versioni Go sono disponibili nel
[pacchetto di build Go](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.8.6){: new_window}
attualmente installato in {{site.data.keyword.Bluemix_notm}}:

* 1.6.3
* 1.6.4
* 1.7.5
* 1.7.6
* 1.8.1
* 1.8.3

Se la tua applicazione richiede una versione di Go che non è elencata, puoi utilizzare
il [pacchetto di build Go](https://github.com/cloudfoundry/go-buildpack.git){: new_window}
esterno per distribuire l'applicazione.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}

* [GoLang](http://golang.org/){: new_window}
* [Pacchetto di build Cloud Foundry per Go](https://github.com/cloudfoundry/go-buildpack){: new_window}
