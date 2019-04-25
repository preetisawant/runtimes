---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-21"
subcollection: "PHP"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}

Il runtime PHP su {{site.data.keyword.Bluemix}} si avvale del php_buildpack.
Il php_buildpack fornisce un ambiente di runtime completo per le applicazioni PHP.
{: shortdesc}

Il php_buildpack viene utilizzato nelle seguenti condizioni:
* La tua applicazione contiene un file composer.json oppure
* la tua applicazione contiene un file *.php oppure
* La tua applicazione definisce una variabile ${WEBDIR} nel suo file [options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html) e tale variabile viene impostata su una directory esistente all'interno della tua applicazione.

## Applicazione starter
{: #starter_application}

{{site.data.keyword.Bluemix}} fornisce un'applicazione starter PHP.  L'applicazione starter PHP è una semplice applicazione PHP che fornisce un template che puoi utilizzare per la tua applicazione. Puoi fare delle prove con l'applicazione starter, apportare modifiche ed eseguirne il push
all'ambiente {{site.data.keyword.Bluemix}}.  Consulta il documento relativo all'[utilizzo delle applicazioni starter](docs/runtimes-common/starter_app_usage.html) per assistenza nell'utilizzo dell'applicazione starter.

## Forza HTTPS in tutte le pagine della tua applicazione
{: #enforce_https}

Per forzare l'utilizzo di HTTPS invece di HTTP in tutte le pagine della tua applicazione quando viene eseguita in {{site.data.keyword.Bluemix_notm}} utilizzando Apache, devono essere effettuate le seguenti modifiche al tuo file ".htaccess".  Questa regola sarà applicata a tutte le richieste che non sono state effettuate utilizzando HTTPS solo quando in esecuzione in {{site.data.keyword.Bluemix_notm}}.

```
RewriteCond %{HTTP:X-Forwarded-Proto} !=https [NC]
RewriteCond %{ENV:BLUEMIX_REGION} !^$
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

## Versioni di runtime
{: #runtime_versions}

Puoi specificare la versione di PHP che deve essere utilizzata dalla tua applicazione nel file composer.json. Ad esempio:

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
Per ulteriori informazioni, consulta [Composer Package links  ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://getcomposer.org/doc/04-schema.md#package-links).

Quando non viene specificata una versione, viene scelta per impostazione predefinita la versione 5.6.34.

### Versioni disponibili:
{: #available_versions}

Le seguenti versioni PHP sono disponibili nel [pacchetto
di build PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.51) attualmente installato
in {{site.data.keyword.Bluemix}}:

* 5.6.33
* 5.6.34
* 7.0.27
* 7.0.28
* 7.1.14
* 7.1.15
* 7.2.2
* 7.2.3

Se la tua applicazione richiede una versione di PHP che non è elencata,
puoi utilizzare il [pacchetto
di build PHP](https://github.com/cloudfoundry/php-buildpack.git) esterno per distribuire l'applicazione.
