---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-05"
subcollection: "Ruby"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Ruby
{: #ruby_runtime}

Il runtime Ruby su {{site.data.keyword.Bluemix}} si avvale del ruby_buildpack.
Il ruby_buildpack fornisce un ambiente di runtime completo per le applicazioni Ruby.
{: shortdesc}

Il ruby_buildpack viene utilizzato se la tua applicazione ha un Gemfile nella directory root. Utilizzerà quindi Bundler per installare le tue dipendenze.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} Fornisce un'applicazione starter Ruby.  L'applicazione starter Ruby è una semplice applicazione Ruby che fornisce un template che puoi utilizzare per la tua applicazione. Puoi fare delle prove con l'applicazione starter, apportare modifiche ed eseguirne il push
all'ambiente {{site.data.keyword.Bluemix_notm}}.  Consulta [Utilizzo di applicazioni starter](../common/starter_app_usage.html) per informazioni sull'utilizzo dell'applicazione starter.

## Versioni di runtime
{: #runtime_versions}

Puoi specificare la versione di Ruby che deve essere utilizzata dalla tua applicazione nel Gemfile della tua applicazione, ad esempio:

```
  source 'https://rubygems.org'
  ruby '2.5.0'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

Quando non viene specificata una versione, viene scelta per impostazione predefinita la versione 2.4.3.

### Versioni disponibili:
{: #available_versions}

Le seguenti versioni Ruby sono disponibili nel [pacchetto
di build Ruby](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.7.15) attualmente installato
in {{site.data.keyword.Bluemix}}:

* 2.2.8
* 2.2.9
* 2.3.5
* 2.3.6
* 2.4.2
* 2.4.3
* 2.5.0

Se la tua applicazione richiede una versione di Ruby che non è elencata,
puoi utilizzare il [pacchetto
di build Ruby](https://github.com/cloudfoundry/ruby-buildpack) esterno per distribuire l'applicazione.
