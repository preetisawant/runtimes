---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}

L'environnement d'exécution Go dans {{site.data.keyword.Bluemix}} repose sur le pack go_buildpack.
Le pack go_buildpack fournit un environnement d'exécution complet pour les applis Go.
{: shortdesc}

Le pack go_buildpack est utilisé si votre application contient un fichier nommé *.go.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} propose une application de démarrage Go.  Il s'agit d'une appli Go simple qui fournit un modèle que vous pouvez utiliser pour votre appli. Vous pouvez l'utiliser pour faire des essais, faire des modifications et les envoyer par commande push vers l'environnement {{site.data.keyword.Bluemix_notm}}. Consultez [Utilisation des applications de démarrage](../common/starter_app_usage.html) pour obtenir de l'aide sur l'application de démarrage.

## Versions d'environnement d'exécution
{: #runtime_versions}

Vous pouvez spécifier la version de Go à utiliser par votre appli en définissant la propriété GoVersion dans le fichier Godeps/Godeps.json qui se trouve à la racine de votre appli. Par exemple :

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.10",
	"Deps": []
}
```
{: codeblock}
Pour plus d'informations, voir [godep](https://github.com/tools/godep){: new_window}.

Si aucune version n'est spécifiée, la version 1.8.7 est sélectionnée par défaut.

### Versions disponibles :
{: #available_versions}

Les versions de Go suivantes sont disponibles dans le [pack de construction Go](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.8.20){: new_window} qui est installé dans {{site.data.keyword.Bluemix_notm}} :

* 1.6.3
* 1.6.4
* 1.7.5
* 1.7.6
* 1.8.6
* 1.8.7
* 1.9.3
* 1.9.4
* 1.10

Si votre application requiert une version de Go qui n'est pas répertoriée ci-dessus, vous pouvez utiliser le [pack de construction Go](https://github.com/cloudfoundry/go-buildpack.git){: new_window} externe pour déployer l'application.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}

* [GoLang](http://golang.org/){: new_window}
* [Cloud Foundry buildpack for Go](https://github.com/cloudfoundry/go-buildpack){: new_window}
