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

Die Laufzeit von PHP in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'php_buildpack'.
Das Buildpack 'php_buildpack' stellt eine vollständige Laufzeitumgebung für PHP-Apps zur Verfügung.
{: shortdesc}

Das Buildpack 'php_buildpack' wird unter folgenden Bedingungen verwendet:
* Ihre App enthält die Datei 'composer.json' oder
* Ihre App enthält eine '*.php'-Datei oder
* Ihre App definiert die Variable ${WEBDIR} in ihrer Datei [options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html) und als Einstellung für diese Variable ist ein in Ihrer App vorhandenes Verzeichnis festgelegt.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine PHP-Starter-App zur Verfügung.  Die PHP-Starteranwendung ist eine einfache PHP-App, die Sie als Vorlage für Ihre App verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der {{site.data.keyword.Bluemix}}-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starter-App finden Sie in [Starteranwendungen verwenden](docs/runtimes-common/starter_app_usage.html).

## HTTPS auf allen Seiten in Ihrer Anwendung erzwingen
{: #enforce_https}

Wenn bei der Ausführung Ihrer Anwendung in {{site.data.keyword.Bluemix_notm}} mithilfe von Apache auf allen Seiten HTTPS anstatt HTTP erzwungen werden soll, müssen Sie an der ".htaccess"-Datei die folgenden Änderungen vornehmen.  Diese Regel gilt für jede Anforderung, die nicht mithilfe von HTTPS abgesetzt wurde und nur bei Ausführung in {{site.data.keyword.Bluemix_notm}}.

```
RewriteCond %{HTTP:X-Forwarded-Proto} !=https [NC]
RewriteCond %{ENV:BLUEMIX_REGION} !^$
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

## Laufzeitversionen
{: #runtime_versions}

Sie können die Version von PHP, die von Ihrer App verwendet werden soll, in der Datei 'composer.json' angeben. Beispiel:

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
Weitere Informationen finden Sie unter [Composer-Paketlinks ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://getcomposer.org/doc/04-schema.md#package-links).

Wenn keine Version angegeben ist, wird standardmäßig Version 5.6.34 ausgewählt.

### Verfügbare Versionen:
{: #available_versions}

Folgende PHP-Versionen stehen im [PHP-Buildpack](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.51) zur Verfügung, das zurzeit in {{site.data.keyword.Bluemix}} installiert ist:

* 5.6.33
* 5.6.34
* 7.0.27
* 7.0.28
* 7.1.14
* 7.1.15
* 7.2.2
* 7.2.3

Wenn für Ihre App eine PHP-Version erforderlich ist, die nicht aufgelistet ist, können Sie die App mit dem externen [PHP-Buildpack](https://github.com/cloudfoundry/php-buildpack.git) implementieren.
