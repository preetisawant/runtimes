---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Ruby
{: #ruby_runtime}

Die Laufzeit von Ruby in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'ruby_buildpack'.
Das Buildpack 'ruby_buildpack' bietet eine vollständige Laufzeitumgebung für Ruby-Apps.
{: shortdesc}

Das Buildpack 'ruby_buildpack' wird verwendet, wenn im Stammverzeichnis Ihrer App das Element 'Gemfile' enthalten ist. Zum Installieren Ihrer Abhängigkeiten wird anschließend Bundler verwendet.

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} stellt eine Ruby-Starteranwendung bereit. Die Ruby-Starteranwendung ist eine einfache Ruby-App, die Sie als Vorlage für Ihre App verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der {{site.data.keyword.Bluemix_notm}}-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starteranwendung finden Sie in [Starteranwendungen verwenden](../common/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die Version von Ruby, die von Ihrer App verwendet werden soll, im Element 'Gemfile' Ihrer Anwendung angeben. Beispiel:

```
  source 'https://rubygems.org'
  ruby '2.4.1'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

Wenn keine Version angegeben ist, wird standardmäßig Version 2.4.1 ausgewählt.

### Verfügbare Versionen:
{: #available_versions}

Folgende Ruby-Versionen stehen im [Ruby-Buildpack](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.34) zur Verfügung, das zurzeit in {{site.data.keyword.Bluemix}} installiert ist:

* 2.1.8
* 2.1.9
* 2.2.6
* 2.2.7
* 2.3.3
* 2.3.4
* 2.4.0
* 2.4.1

Wenn für Ihre App eine Ruby-Version erforderlich ist, die nicht aufgelistet ist, können Sie die App mit dem externen [Ruby-Buildpack](https://github.com/cloudfoundry/ruby-buildpack) implementieren.

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Cloud Foundry-Buildpack für Ruby](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Dokumentation zu Ruby on Rails ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://api.rubyonrails.org/)
