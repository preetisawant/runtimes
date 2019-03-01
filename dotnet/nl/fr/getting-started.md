---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-05"

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
{: #getting_started}

* {: download} Félicitations, vous avez déployé une application exemple Hello World sur {{site.data.keyword.Bluemix}} !  Pour commencer, suivez ce guide pas à pas. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Télécharger l'exemple de code)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Télécharger le code de l'application" />téléchargez l'exemple de code</a> et découvrez-le par vous-même.

En suivant ce tutoriel d'initiation, vous allez configurer un environnement de développement, déployer une application localement et sur {{site.data.keyword.Bluemix}}, puis intégrer un service de base de données {{site.data.keyword.Bluemix}} dans votre application.

## Avant de commencer
{: #prereqs}

Vous aurez besoin des éléments suivants :
* [Compte {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} interface de ligne de commande](/docs/cli/reference/ibmcloud/download_cli.html)
* [Git ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://git-scm.com/downloads){: new_window}
* Installez .NET Core 2.1.1 SDK 2.1.301 depuis le [site Web de téléchargement .NET Core ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.microsoft.com/net/download/core).

## Etape 1 : Cloner l'application exemple
{: #clone}

Commencez par cloner le référentiel GitHub contenant l'application exemple.
  ```
git clone https://github.com/IBM-Cloud/get-started-aspnet-core
  ```
  {: codeblock}


## Etape 2 : Exécuter l'application localement
{: #run_locally}

1. Sur la ligne de commande, placez-vous dans le répertoire où se trouve l'application exemple.

  ```
  cd get-started-aspnet-core/src/GetStartedDotnet
  ```
  {: codeblock}

1. Exécutez l'application en local en exécutant les commandes suivantes.

  ```
dotnet restore
  ```
  {: codeblock}

  ```
dotnet run
  ```
  {: codeblock}

1. Affichez votre application sur : http://localhost:5000/.

## Etape 3 : Préparer l'application pour le déploiement
{: #prepare}

Pour déployer sur {{site.data.keyword.Bluemix_notm}}, il peut être utile de créer un fichier manifest.yml. Ce fichier inclut des informations essentielles sur votre application, telles que son nom, la quantité de mémoire à allouer à chaque instance et la route. Pour vous éviter d'avoir à le créer, nous avons prévu un exemple de fichier manifest.yml dans le répertoire `get-started-dotnet`.

Ouvrez le fichier manifest.yml et, dans le champ `name`, remplacez le nom `GetStartedDotnet` par celui de votre application, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedDotnet
   random-route: true
   memory: 512M
  ```
  {: codeblock}

Dans ce fichier manifest.yml, l'effet de **`random-route: true`** est de générer une route aléatoire pour votre application afin d'éviter qu'elle n'entre en conflit avec d'autres.  Au besoin, vous pouvez remplacer **`random-route: true`** par **`host: myChosenHostName`** et fournir un nom d'hôte de votre choix.
{: tip}

## Etape 4 : Déployer l'application
{: #deploy}

Vous pouvez utiliser l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} pour déployer des applications.

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

1. **Assurez-vous d'être dans le répertoire principal de votre application, `get-started-aspnet-core`**, puis envoyez votre application par commande push vers {{site.data.keyword.Bluemix_notm}}
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

## Etape 6 : Utiliser la base de données localement
{: #use_database}

Nous allons à présent mettre à jour votre code local pour le faire pointer sur cette base de données. Créons à cet effet un fichier JSON pour y stocker les identifiants d'accès aux services. Ce fichier ne sera utilisé QUE lorsque l'application est exécutée localement. Lors de son fonctionnement sur {{site.data.keyword.Bluemix_notm}}, elle obtiendra ces identifiants en lisant la variable d'environnement `VCAP_SERVICES`.

1. Dans le répertoire `src/GetStartedDotnet`, créez un fichier `vcap-local.json`.

1. Copiez et collez l'objet JSON suivant dans le fichier `vcap-local.json`, puis sauvegardez vos modifications.

   ```json
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

1. Recherchez votre application dans la [liste de ressources](https://cloud.ibm.com/resources) {{site.data.keyword.Bluemix_notm}}. Sur la page de détails du service de votre application, cliquez sur **Connections** dans la barre d'options latérale. Cliquez sur l'icône de menu {{site.data.keyword.cloudant_short_notm}} (**&hellip;**) et sélectionnez **Afficher les données d'identification**.

1. Copiez seulement la valeur `url` des données d'identification et collez-la dans le champ `url` du fichier `vcap-local.json` pour remplacer `CLOUDANT_DATABASE_URL`.

1. Depuis le répertoire `get-started-aspnet-core/src/GetStartedDotnet`, redémarrez votre application en exécutant la commande suivante.

   ```
   dotnet run
   ```
   {: codeblock}

1. Dans votre navigateur, actualisez la vue de http://localhost:5000/. Chaque nom que vous entrez dans l'application sera ajouté à la base de données.

Votre application locale et l'application {{site.data.keyword.Bluemix_notm}} partagent la base de données.  Affichez votre application {{site.data.keyword.Bluemix_notm}} en accédant à l'URL qui figure dans la sortie de la commande `ibmcloud cf push`.  Les noms que vous ajoutez depuis l'une ou l'autre version de l'application doivent apparaître dans les deux lorsque vous actualisez les navigateurs.

Si vous n'avez pas besoin de votre application live, arrêtez-la. Vous éviterez des frais imprévus.
{: tip}

## Etapes suivantes

* [Tutoriels](/docs/tutorials/index.html)
* [Exemples ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
