---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}

L'environnement d'exécution PHP dans {{site.data.keyword.Bluemix}} repose sur le pack php_buildpack.
Le pack php_buildpack fournit un environnement d'exécution complet pour les applis PHP.
{: shortdesc}

Le pack php_buildpack est utilisé dans les conditions suivantes :
* votre appli contient un fichier composer.json, ou
* votre appli contient un fichier *.php, ou
* votre appli définit une variable ${WEBDIR} dans son fichier [options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html) et cette variable a pour valeur un répertoire existant dans votre appli.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} propose une application de démarrage PHP.  L'application de démarrage PHP est une appli PHP simple qui fournit un modèle que vous pouvez utiliser pour votre appli. Vous pouvez expérimenter cette application et effectuer des modifications puis les envoyer par commande push vers l'environnement {{site.data.keyword.Bluemix}}.  Voir [Utilisation des applications de démarrage](docs/runtimes-common/starter_app_usage.html) pour obtenir de l'aide.

## Imposer l'utilisation de HTTPS sur toutes les pages dans votre application
{: #enforce_https}

Pour imposer l'utilisation de HTTPS au lieu de HTTP sur toutes les pages dans votre application lorsqu'elle s'exécute dans {{site.data.keyword.Bluemix_notm}} avec Apache, les modifications suivantes doivent être effectuées dans le fichier ".htaccess".  Cette règle s'appliquera à toutes les demandes qui n'ont pas été effectuées avec HTTPS uniquement lors d'une exécution dans {{site.data.keyword.Bluemix_notm}}.

```
RewriteCond %{HTTP:X-Forwarded-Proto} !=https [NC]
RewriteCond %{ENV:BLUEMIX_REGION} !^$
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

## Versions d'environnement d'exécution
{: #runtime_versions}

Vous pouvez spécifier la version de PHP que votre application doit utiliser en utilisant le fichier composer.json. Par exemple :

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
Pour plus d'informations, voir les [liens Composer Package![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://getcomposer.org/doc/04-schema.md#package-links).

Si aucune version n'est spécifiée, la version 5.6.34 est sélectionnée par défaut.

### Versions disponibles :
{: #available_versions}

Les versions de PHP suivantes sont disponibles dans le [pack de construction PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.51) qui est installé dans {{site.data.keyword.Bluemix}} :

* 5.6.33
* 5.6.34
* 7.0.27
* 7.0.28
* 7.1.14
* 7.1.15
* 7.2.2
* 7.2.3

Si votre application requiert une version de PHP qui n'est pas répertoriée, vous pouvez utiliser le [pack de construction PHP](https://github.com/cloudfoundry/php-buildpack.git) externe pour la déployer.
