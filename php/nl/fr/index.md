---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-17"

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

{{site.data.keyword.Bluemix}} propose une application de démarrage PHP.  L'application de démarrage PHP est une appli PHP simple qui fournit un modèle que vous pouvez utiliser pour votre appli. Vous pouvez expérimenter cette application et effectuer des modifications puis les envoyer par commande push vers l'environnement {{site.data.keyword.Bluemix}}.  Voir [Utilisation des applications de démarrage](/docs/cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Imposer l'utilisation de HTTPS sur toutes les pages dans votre application
{: #enforce_https}

Pour imposer l'utilisation de HTTPS au lieu de HTTP sur toutes les pages dans votre application lorsqu'elle s'exécute dans Bluemix avec Apache, les modifications suivantes doivent être effectuées dans le fichier ".htaccess". Cette règle s'appliquera à toutes les demandes qui n'ont pas été effectuées avec HTTPS uniquement lors d'une exécution dans Bluemix.

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
Pour plus d'informations, voir les [liens Composer Package![External link icon](../../icons/launch-glyph.svg "External link icon")](https://getcomposer.org/doc/04-schema.md#package-links).

Si aucune version n'est spécifiée, la version 5.5.38 est sélectionnée par défaut.

### Versions disponibles :
{: #available_versions}

Les versions de PHP suivantes sont disponibles dans le [pack de construction PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.27) qui est installé dans {{site.data.keyword.Bluemix}} :

* 5.5.37
* 5.5.38
* 5.6.29
* 5.6.30
* 7.0.14
* 7.0.15
* 7.1.0
* 7.1.1

Si votre application requiert une version de PHP qui n'est pas répertoriée, vous pouvez
utiliser le [pack de construction PHP](https://github.com/cloudfoundry/php-buildpack.git) externe pour
la déployer.

# rellinks
{: #rellinks notoc}
## Tutoriels et exemples
{: #samples notoc}
* [Build and deploy a REST API](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Build and deploy a mobile-friendly calorie counter ](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## general
{: #general notoc}
* [Cloud Foundry buildpack for PHP](https://github.com/cloudfoundry/php-buildpack.git)
