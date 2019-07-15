---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Ruby
{: #ruby_runtime}

L'environnement d'exécution Ruby dans {{site.data.keyword.Bluemix}} repose sur le pack ruby_buildpack.
Le pack ruby_buildpack fournit un environnement d'exécution complet pour les applis Ruby.
{: shortdesc}

Le pack ruby_buildpack est utilisé si votre appli comporte un fichier Gemfile dans son répertoire racine. Il utilisera alors un programme de mise en bundle pour installer vos dépendances.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} propose une application de démarrage Ruby.  L'application de démarrage Ruby est une appli Ruby simple qui fournit un modèle que vous pouvez utiliser pour votre appli. Vous pouvez expérimenter cette application et effectuer des modifications puis les envoyer par commande push vers l'environnement {{site.data.keyword.Bluemix_notm}}.  Voir [Utilisation des applications de démarrage](../common/starter_app_usage.html) pour obtenir de l'aide.

## Versions d'environnement d'exécution
{: #runtime_versions}

Vous pouvez spécifier la version de Ruby à utiliser par votre application dans le fichier Gemfile de votre application. Exemple :

```
  source 'https://rubygems.org'
  ruby '2.4.1'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

Si aucune version n'est spécifiée, la version 2.4.3 est sélectionnée par défaut.

### Versions disponibles :
{: #available_versions}

Les versions de Ruby suivantes sont disponibles dans le [pack de construction Ruby](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.7.15) qui est installé dans {{site.data.keyword.Bluemix}} :

* 2.2.8
* 2.2.9
* 2.3.5
* 2.3.6
* 2.4.2
* 2.4.3
* 2.5.0

Si votre application requiert une version de Ruby qui n'est pas répertoriée, vous pouvez utiliser le [pack de construction Ruby](https://github.com/cloudfoundry/ruby-buildpack) externe pour la déployer.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Cloud Foundry buildpack for Ruby](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Documentation de Ruby on Rails ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://api.rubyonrails.org/)
