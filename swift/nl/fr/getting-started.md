---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-05"
subcollection: "Swift"

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
{: #getting-started}

* {: download} Félicitations, vous avez déployé une application exemple Hello World sur {{site.data.keyword.Bluemix}} !  Pour commencer, suivez ce guide pas à pas. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Télécharger l'exemple de code)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Télécharger le code de l'application" />téléchargez l'exemple de code</a> et découvrez-le par vous-même.

En suivant ce tutoriel, vous allez configurer un environnement de développement, déployer une application à la fois localement et sur {{site.data.keyword.Bluemix}}, puis intégrer un service de base de données {{site.data.keyword.Bluemix_notm}} dans votre application.

Tout au long de ces documents, les références à l'interface CLI Cloud Foundry sont désormais mis à jour dans l'interface CLI de {{site.data.keyword.Bluemix_notm}}. L'interface CLI {{site.data.keyword.Bluemix_notm}} possède les mêmes commandes Cloud Foundry familières, mais avec une meilleure intégration aux comptes et autres services {{site.data.keyword.Bluemix_notm}}. Ce tutoriel vous permet d'en apprendre davantage sur l'initiation à l'interface CLI {{site.data.keyword.Bluemix_notm}}.
{: tip}

## Avant de commencer
{: #prereqs}
* [Git ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://git-scm.com/downloads){: new_window}
* [{{site.data.keyword.Bluemix_notm}} interface de ligne de commande](/docs/cli/reference/ibmcloud/download_cli.html)
* [Compilateur Swift ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://swift.org/download/) pour votre plateforme.

## Etape 1 : Cloner l'application exemple
{: #clone}

Commencez par cloner le référentiel et placez-vous dans le répertoire où se trouve l'application exemple.
  ```
git clone https://github.com/IBM-Cloud/get-started-swift
  ```
  {: codeblock}

  ```
cd get-started-swift
  ```
  {: codeblock}

  Examinez attentivement les fichiers dans le répertoire *get-started-swift* afin de vous familiariser avec leur contenu.

## Etape 2 : Exécuter l'application localement
{: #run_locally}

Ayant installé le compilateur Swift et cloné ce référentiel Git, vous pouvez à présent compiler et exécuter l'application.

1. Accédez au répertoire racine de ce référentiel sur votre système et émettez la commande suivante :

  ```
swift build
  ```
  {: codeblock}

  Cette commande peut prendre quelques minutes pour s'exécuter.

1. Une fois l'application correctement compilée, vous pouvez lancer l'exécutable qui a été généré par le compilateur Swift :
```
swift run
```
  {: codeblock}

  ou
  ```
.build/debug/get-started-swift
  ```
  {: codeblock}

  Vous devriez obtenir un résultat semblable au suivant :

  ```
Server is listening on port: 8080
  ```
  {: pre}

1. Affichez votre application sur l'URL suivante : http://localhost:8080

## Etape 3 : Préparer l'application pour le déploiement
{: #prepare}

Pour déployer sur {{site.data.keyword.Bluemix_short}}, il peut être utile de créer un fichier manifest.yml. Ce fichier inclut des informations essentielles sur votre application, telles que son nom, la quantité de mémoire à allouer à chaque instance et la route. Pour vous éviter d'avoir à le créer, nous avons prévu un exemple de fichier manifest.yml dans le répertoire `get-started-swift`.

Ouvrez le fichier manifest.yml et, dans le champ `name`, remplacez le nom `GetStartedSwift` par celui de votre application, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: Get-Started-Swift
     random-route: true
     memory: 256M
     command: get-started-swift
     buildpack: swift_buildpack
  ```
  {: codeblock}

Dans ce fichier manifest.yml, l'effet de **random-route: true** est de générer une route aléatoire pour votre application afin d'éviter qu'elle n'entre en conflit avec d'autres.  Au besoin, vous pouvez remplacer **random-route: true** par **host: myChosenHostName** et fournir un nom d'hôte de votre choix.
{: tip}

## Etape 4 : Déployer l'application
{: #deploy}

Vous pouvez utiliser l'interface de ligne de commande {{site.data.keyword.Bluemix_short}} pour déployer des applications.

1. Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}} et sélectionnez un point de terminaison d'API.

  ```
ibmcloud login
  ```
  {: codeblock}

  Si vous possédez un ID utilisateur fédéré, utilisez la commande suivante à la place afin de vous connecter avec votre ID de connexion unique. Voir [Connexion à l'aide d'un ID fédéré](/docs/cli/login_federated_id.html) pour en savoir plus.

  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Ciblez une organisation et un espace Cloud Foundry :
  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Si vous ne disposez pas d'une organisation ou d'un espace configuré, voir [Ajout d'organisations et d'espaces](/docs/account/orgs_spaces.html).
  {: tip}

1. Depuis le répertoire *get-started-swift*, envoyez votre application par commande push à {{site.data.keyword.Bluemix_notm}}

  ```
ibmcloud cf push
  ```
  {: codeblock}

  Cette opération peut prendre une minute. En cas d'erreur dans le processus de déploiement, vous pouvez utiliser la commande `ibmcloud cf logs <Your-App-Name> --recent` pour identifier et résoudre le problème.

Une fois le déploiement achevé, vous devez voir un message indiquant que votre application est lancée.  Vous pouvez visualiser l'application en accédant à l'URL qui figure dans la sortie de la commande push.  Vous pouvez aussi émettre la commande suivante pour voir l'état de votre application et obtenir son URL.

  ```
ibmcloud cf apps
  ```
  {: codeblock}

Vous pouvez également accéder à la [liste de ressources](https://cloud.ibm.com/resources) {{site.data.keyword.Bluemix_notm}} pour afficher votre application.

## Etape 5 : Ajouter une base de données
{: #add_database}

Nous allons à présent ajouter une base de données {{site.data.keyword.cloudant_short_notm}} NoSQL à l'application et configurer cette dernière pour qu'elle puisse être exécutée localement et sur {{site.data.keyword.Bluemix_notm}}.

1. Dans votre navigateur, connectez-vous à {{site.data.keyword.Bluemix_notm}} et allez au Tableau de bord. Sélectionnez **Créer une ressource**.
1. Recherchez **{{site.data.keyword.cloudant_short_notm}}** puis sélectionnez le service.
1. Pour les **méthodes d'authentification disponibles**, sélectionnez **Utiliser les données d'identification existantes et IAM**. Vous pouvez conserver les paramètres par défaut pour les autres zones. Cliquez sur **Créer** pour créer le service.
1. Dans la zone de navigation, accédez à **Connections**, puis cliquez sur **Créer une connexion**. Sélectionnez votre application, puis cliquez sur **Connecter**.
1. En utilisant les valeurs par défaut, cliquez sur **Connecter et reconstituer l'application** pour connecter la base de données à votre application. Cliquez sur **Reconstituer** lorsque vous y êtes invité.

   {{site.data.keyword.Bluemix_notm}} redémarre votre application et lui fournit les données d'identification pour l'accès à la base de données en utilisant la variable d'environnement `VCAP_SERVICES`. L'application n'a accès à cette variable d'environnement que lorsqu'elle fonctionne sur {{site.data.keyword.Bluemix_notm}}.

Les variables d'environnement vous permettent de séparer les paramètres de déploiement de votre code source. Par exemple, au lieu de coder en dur un mot de passe de base de données, vous pouvez le stocker dans une variable d'environnement que vous référencez dans votre code source.
{: tip}

## Etape 6 : Utiliser la base de données
{: #use_database}

Nous allons à présent mettre à jour votre code local pour le faire pointer sur cette base de données. Créons à cet effet un fichier JSON pour y stocker les identifiants d'accès aux services que l'application utilisera. Ce fichier ne sera utilisé QUE lorsque l'application est exécutée localement. Lors de son fonctionnement sur {{site.data.keyword.Bluemix_notm}}, elle obtiendra ces identifiants en lisant la variable d'environnement VCAP_SERVICES.

Créez un fichier nommé `my-cloudant-credentials.json` dans le répertoire `config` et ajoutez-y le contenu suivant (référez-vous à `config/my-cloudant-credentials.json.example`) :

 ```
 {
   "password": "<password>",
   "url": "<url>",
   "username": "<username>"
 }
 ```
 {: codeblock}

Modifiez le fichier `mappings.json` dans le répertoire `config` en remplaçant `cloudant` par le **nom** de votre instance de base de données :

  ```
{
  "MyCloudantDB": {
    "searchPatterns": [
      "cloudfoundry:cloudant",
      "env:kube-cloudant-credentials",
      "file:config/my-cloudant-credentials.json"
    ]
  }
}
  ```
  {: codeblock}

Cette application exemple utilise le package `CloudEnvironment` pour interagir avec {{site.data.keyword.Bluemix_notm}} en vue d'interpréter les variables d'environnement. [En savoir plus...](https://github.com/IBM-Swift/CloudEnvironment)

L'emplacement réservé `cloudant`, dans la configuration `cloudfoundry:cloudant`, facilite l'association d'un service Cloudant fourni par l'utilisateur à votre application. Avec la configuration `cloudfoundry:cloudant`, vous pouvez créer un service Cloudant incluant la chaîne `cloudant` quelque part dans son nom et l'associer à votre application sans avoir besoin d'éditer le fichier `config.json`. Si vous modifiez cette configuration et que vous souhaitez plus tard utiliser un service Cloudant fourni par vous-même, vous devrez soit éditer la configuration pour y inclure `cloudfoundry:cloudant`, soit définir `cloudfoundry:` avec le nom de votre service.
{: tip}

Recherchez votre application dans la [liste de ressources](https://cloud.ibm.com/resources) {{site.data.keyword.Bluemix_notm}}. Sur la page de détails du service de votre application, cliquez sur **Connections** dans la barre d'options latérale. Cliquez sur l'icône de menu {{site.data.keyword.cloudant_short_notm}} (**&hellip;**) et sélectionnez **Afficher les données d'identification**.

Copiez les données d'identification (et seulement elles) et collez-les dans les champs correspondants de votre fichier config.json local.

Construisez et lancez votre application localement.
 ```
swift build  
 ```
 {: codeblock}

  ```
.build/debug/kitura-helloworld
  ```
 {: codeblock}

 Affichez votre application sur : http://localhost:8080. Chaque nom que vous entrez dans l'application sera ajouté à la base de données.

 Cet exemple d'application utilise le package `Kitura-CouchDB` pour interagir avec Cloudant. [En savoir plus...](https://github.com/IBM-Swift/Kitura-CouchDB)

 Apportez les changements voulus et redéployez sur {{site.data.keyword.Bluemix_notm}}!

  ```
ibmcloud cf app push
  ```

Vous pouvez visualiser l'application en accédant à l'URL qui figure dans la sortie de la commande push. Par exemple, *myUrl.mybluemix.net*.

Si vous n'avez pas besoin de votre application live, arrêtez-la. Vous éviterez des frais imprévus.
{: tip}

## Etapes suivantes

* [Kitura et tutoriels Swift côté serveur ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.kitura.io/learn.html){: new_window}
* [Exemples ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
