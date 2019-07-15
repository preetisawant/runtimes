---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-03"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}


# Tutoriel Initiation

* {: download} Félicitations, vous avez déployé une application exemple Hello World sur {{site.data.keyword.Bluemix}} !  Pour commencer, suivez ce guide pas à pas. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Télécharger l'exemple de code)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Télécharger le code de l'application" />téléchargez l'exemple de code</a> et découvrez-le par vous-même.

En suivant ce tutoriel, vous allez configurer un environnement de développement, déployer une application à la fois localement et sur {{site.data.keyword.Bluemix}}, puis intégrer un service de base de données {{site.data.keyword.Bluemix_notm}} dans votre application.

Tout au long de ces documents, les références à l'interface CLI Cloud Foundry sont désormais mis à jour dans l'interface CLI de {{site.data.keyword.Bluemix_notm}}. L'interface CLI {{site.data.keyword.Bluemix_notm}} possède les mêmes commandes Cloud Foundry familiaires, mais avec une meilleure intégration aux comptes et autres services {{site.data.keyword.Bluemix_notm}}. Ce tutoriel vous permet d'en apprendre davantage sur l'initiation à l'interface CLI {{site.data.keyword.Bluemix_notm}}.
{: tip}

## Avant de commencer
{: #prereqs}

Vous aurez besoin des comptes et outils suivants :
* [Compte {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [Interface CLI {{site.data.keyword.Bluemix_notm}}](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://git-scm.com/downloads){: new_window}
* [Node ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://nodejs.org/en/){: new_window}


## Etape 1 : Cloner l'application exemple
{: #clone}

Commencez par cloner le référentiel GitHub contenant l'application exemple Node.js *hello world*.
  ```
git clone https://github.com/IBM-Cloud/get-started-node
  ```
  {: codeblock}

## Etape 2 : Exécuter l'application localement
{: #run_locally}

Utilisez le gestionnaire de package npm pour installer les dépendances et lancer votre application.

1. Sur la ligne de commande, placez-vous dans le répertoire où se trouve l'application exemple.
  ```
cd get-started-node
  ```
  {: codeblock}

1. Installez les dépendances listées dans le fichier [package.json ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.npmjs.com/files/package.json) afin de pouvoir exécuter l'application localement.  
  ```
npm install
  ```
  {: codeblock}

1. Exécutez l'application.
  ```
npm start  
  ```
  {: codeblock}

1. Affichez votre application sur l'URL suivante : http://localhost:3000

Utilisez [nodemon](https://nodemon.io/) pour que l'application redémarre automatiquement en cas de changement de fichier.
{: tip}

## Etape 3 : Préparer l'application pour le déploiement
{: #prepare}

Pour déployer sur {{site.data.keyword.Bluemix_notm}}, il peut être utile de créer un fichier manifest.yml. Ce fichier inclut des informations essentielles sur votre application, telles que son nom, la quantité de mémoire à allouer à chaque instance et la route. Pour vous éviter d'avoir à le créer, nous avons prévu un exemple de fichier manifest.yml dans le répertoire `get-started-node`.

Ouvrez le fichier manifest.yml et, dans le champ `name`, remplacez le nom `GetStartedNode` par celui de votre application, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

```
applications:
- name: GetStartedNode
  random-route: true
  memory: 128M
```
{: codeblock}

Dans ce fichier manifest.yml, l'effet de **random-route: true** est de générer une route aléatoire pour votre application afin d'éviter qu'elle n'entre en conflit avec d'autres.  Au besoin, vous pouvez remplacer **random-route: true** par **host: myChosenHostName** et fournir un nom d'hôte de votre choix.
{: tip}

## Etape 4 : Déployer l'application
{: #deploy}

Pour déployer des applications sur {{site.data.keyword.Bluemix_notm}}, vous pouvez utiliser le client de ligne de commande pour {{site.data.keyword.Bluemix_notm}}.

1. Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}} et sélectionnez un point de terminaison d'API.
  ```
ibmcloud login
  ```
  {: codeblock}

  Si vous possédez un ID utilisateur fédéré, utilisez la commande suivante à la place afin de vous connecter avec votre ID de connexion unique. Voir [Connexion à l'aide d'un ID fédéré](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) pour en savoir plus.
  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Ciblez une organisation et un espace Cloud Foundry :

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Si vous ne disposez pas d'une organisation ou d'un espace configuré, voir [Ajout d'organisations et d'espaces](https://console.bluemix.net/docs/account/orgs_spaces.html).
    {: tip}

1. Depuis le répertoire *get-started-node*, envoyez votre application par commande push vers {{site.data.keyword.Bluemix_notm}}.

  ```
ibmcloud cf push
  ```
  {: codeblock}

Le déploiement de votre application peut prendre quelques minutes. Une fois le déploiement achevé, vous verrez un message indiquant que votre application est lancée. Vous pouvez visualiser l'application en accédant à l'URL qui figure dans la sortie de la commande push. Vous pouvez aussi voir à la fois son statut de déploiement et son URL en exécutant la commande suivante :

  ```
ibmcloud cf apps
  ```
  {: codeblock}

Vous pouvez identifier et résoudre les erreurs du processus de déploiement en utilisant la commande `ibmcloud cf logs <Your-App-Name> --recent`.
{: tip}

## Etape 5 : Ajouter une base de données
{: #add_database}

Nous allons à présent ajouter une base de données {{site.data.keyword.cloudant_short_notm}} NoSQL à l'application et configurer cette dernière pour qu'elle puisse être exécutée localement et sur {{site.data.keyword.Bluemix_notm}}.

1. Dans votre navigateur, connectez-vous à {{site.data.keyword.Bluemix_notm}} et allez au Tableau de bord. Sélectionnez **Créer une ressource**.
2. Choisissez la section **Données et analyse**, puis sélectionnez **{{site.data.keyword.cloudant_short_notm}}** et créez votre service.
3. Accédez à la vue **Connexions** et sélectionnez votre application, puis **Créer une connexion**.
4. Sélectionnez **Reconstituer** lorsque vous y êtes invité. {{site.data.keyword.Bluemix_notm}} redémarre votre application et lui fournit les données d'identification pour l'accès à la base de données en utilisant la variable d'environnement `VCAP_SERVICES`. L'application n'a accès à cette variable d'environnement que lorsqu'elle fonctionne sur {{site.data.keyword.Bluemix_notm}}.

Les variables d'environnement vous permettent de séparer les paramètres de déploiement de votre code source. Par exemple, plutôt que de coder en dur le mot de passe d'accès à la base de données, vous pouvez le stocker dans une variable d'environnement et inclure une référence à celle-ci dans votre code source.
{: tip}

## Etape 6 : Utiliser la base de données
{: #use_database}
Nous allons à présent mettre à jour votre code local pour le faire pointer sur cette base de données. Créons à cet effet un fichier JSON pour y stocker les identifiants d'accès aux services que l'application utilisera. Ce fichier ne sera utilisé QUE lorsque l'application est exécutée localement. Lors de son fonctionnement sur {{site.data.keyword.Bluemix_notm}}, elle obtiendra ces identifiants en lisant la variable d'environnement `VCAP_SERVICES`.

1. Dans le répertoire `get-started-node`, créez un fichier nommé `vcap-local.json` et ajoutez-y le contenu suivant :
  ```
  {
    "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "url":"CLOUDANT_DATABASE_URL"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
    }
  }
  ```
  {: codeblock}

2. Dans votre navigateur, accédez au tableau de bord {{site.data.keyword.Bluemix_notm}} et sélectionnez **_votre appli_ > Connexions**. Cliquez sur l'icône de menu {{site.data.keyword.cloudant_short_notm}} (**&vellip;**) et sélectionnez **Afficher les données d'identification**.

3. Copiez seulement la partie `url` des données d'identification et collez-la dans le champ `url` du fichier `vcap-local.json` pour remplacer `CLOUDANT_DATABASE_URL`.

4. Lancez votre application localement.
  ```
npm start  
  ```
  {: codeblock}

  Affichez votre application locale sur : http://localhost:3000. Chaque nom que vous entrez dans l'application sera ajouté à la base de données.

**Évitez les problèmes **: {{site.data.keyword.Bluemix_notm}} définit la variable d'environnement PORT lorsque votre application fonctionne sur le cloud. En revanche, lorsque l'application est exécutée localement, cette variable n'est pas définie et le numéro de port 3000 est utilisé. Pour plus d'informations, consultez [Exécuter votre application localement](runningLocally.html#hints).

  Votre application locale et son instance {{site.data.keyword.Bluemix_notm}} partagent la même base de données. Les noms que vous ajoutez depuis l'une ou l'autre version de l'application doivent apparaître dans les deux lorsque vous actualisez les navigateurs.

Si vous n'avez pas besoin de votre application live sur {{site.data.keyword.Bluemix_notm}}, arrêtez-la. Vous éviterez des frais imprévus.
{: tip}

## Etapes suivantes

* [Tutoriels](/docs/tutorials/index.html)
* [Exemples ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
