---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-05"
subcollection: "liberty"

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

En suivant ce tutoriel d'initiation Liberty for Java, vous allez configurer un environnement de développement, déployer une application localement et sur {{site.data.keyword.Bluemix}}, et intégrer un service de base de données dans votre application.

Tout au long de ces documents, les références à l'interface CLI Cloud Foundry sont désormais mis à jour dans l'interface CLI de {{site.data.keyword.Bluemix_notm}}. L'interface CLI {{site.data.keyword.Bluemix_notm}} possède les mêmes commandes Cloud Foundry familières, mais avec une meilleure intégration aux comptes et autres services {{site.data.keyword.Bluemix_notm}}. Ce tutoriel vous permet d'en apprendre davantage sur l'initiation à l'interface CLI {{site.data.keyword.Bluemix_notm}}.
{: tip}

## Avant de commencer
{: #prereqs}

Vous aurez besoin des comptes et outils suivants :
* [Compte {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} interface de ligne de commande](/docs/cli/reference/ibmcloud/download_cli.html)
* [Git ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://git-scm.com/downloads){: new_window}
* [Maven ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://maven.apache.org/download.cgi){: new_window}

## Etape 1 : Cloner l'application exemple
{: #clone}

Commencez par cloner le référentiel GitHub contenant l'application exemple.

  ```
git clone https://github.com/IBM-Cloud/get-started-java
  ```
  {: codeblock}


## Etape 2 : Exécuter l'application localement en utilisant la ligne de commande
{: #run_locally}

Utilisez Maven pour construire votre code source et exécuter l'application résultante.

1. Sur la ligne de commande, placez-vous dans le répertoire où se trouve l'application exemple.

  ```
cd get-started-java
  ```
  {: codeblock}

1. Utilisez Maven pour installer les dépendances et construire le fichier .war.

  ```
mvn clean install
  ```
  {: codeblock}

1. Exécutez l'application localement sur Liberty.

  ```
mvn install liberty:run-server
  ```
  {: codeblock}

Lorsque vous voyez le message *Le serveur defaultServer est prêt pour une planète plus intelligente.*, vous pouvez voir votre application fonctionner sur http://localhost:9080/GetStartedJava.

Pour arrêter votre application, utilisez la combinaison de touches **Ctrl-C** dans la fenêtre de ligne de commande d'où vous l'avez lancée.

## Etape 3 : Préparer l'application pour le déploiement
{: #prepare}

Pour déployer sur {{site.data.keyword.Bluemix_notm}}, il peut être utile de créer un fichier manifest.yml. Ce fichier inclut des informations essentielles sur votre application, telles que son nom, la quantité de mémoire à allouer à chaque instance et la route. Pour vous éviter d'avoir à le créer, nous avons prévu un exemple de fichier manifest.yml dans le répertoire `get-started-java`.

Ouvrez le fichier manifest.yml et, dans le champ `name`, remplacez le nom `GetStartedJava` par celui de votre application, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

Dans ce fichier manifest.yml, l'effet de **random-route: true** est de générer une route aléatoire pour votre application afin d'éviter qu'elle n'entre en conflit avec d'autres.  Au besoin, vous pouvez remplacer **random-route: true** par **host: myChosenHostName** et fournir un nom d'hôte de votre choix.
{: tip}

## Etape 4 : Déployer sur {{site.data.keyword.Bluemix_notm}}
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

1. Depuis le répertoire `get-started-java`, envoyez votre application par commande push vers {{site.data.keyword.Bluemix_notm}}.

  ```
ibmcloud cf push
  ```
  {: codeblock}

Le déploiement de votre application peut prendre quelques minutes. Une fois le déploiement achevé, un message s'affiche our indiquer que votre application est lancée. Vous pouvez visualiser l'application en accédant à l'URL qui figure dans la sortie de la commande push et en ajoutant "/GetStartedJava" à la fin. Vous pouvez aussi voir à la fois son statut de déploiement et son URL en exécutant la commande suivante :

  ```
ibmcloud cf apps
  ```
  {: codeblock}

Vous pouvez également accéder à la [liste de ressources](https://cloud.ibm.com/resources) {{site.data.keyword.Bluemix_notm}} pour afficher votre application. Si vous cliquez sur **Visite de l'URL de l'application**, n'oubliez pas d'ajouter "/GetStartedJava" à l'URL.

Vous pouvez identifier et résoudre les erreurs du processus de déploiement en utilisant la commande `ibmcloud cf logs GetStartedJava --recent`.
{: tip}  

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
Nous allons à présent mettre à jour votre code local pour le faire pointer sur cette base de données. Créons à cet effet un fichier de propriétés pour y stocker les identifiants d'accès aux services. Ce fichier ne sera utilisé QUE lorsque l'application est exécutée localement. Lors de son fonctionnement sur {{site.data.keyword.Bluemix_notm}}, elle obtiendra ces identifiants en lisant la variable d'environnement `VCAP_SERVICES`.

1. Recherchez votre application dans la [liste de ressources](https://cloud.ibm.com/resources) {{site.data.keyword.Bluemix_notm}}. Sur la page de détails du service de votre application, cliquez sur **Connections** dans la barre d'options latérale. Cliquez sur l'icône de menu {{site.data.keyword.cloudant_short_notm}} (**&hellip;**) et sélectionnez **Afficher les données d'identification**.

2. Copiez seulement la partie `url` des données d'identification et collez-la dans le champ `url` du fichier `src/main/resources/cloudant.properties`, puis sauvegardez les changements.

  ```
cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:codeblock}

3. Redémarrez le serveur.

Dans votre navigateur, actualisez la vue de http://localhost:9080/GetStartedJava/. Chaque nom que vous entrez dans l'application sera ajouté à la base de données.

Votre application locale et son instance {{site.data.keyword.Bluemix_notm}} partagent la même base de données. Les noms que vous ajoutez depuis l'une ou l'autre version de l'application doivent apparaître dans les deux lorsque vous actualisez les navigateurs.

Si vous n'avez pas besoin de votre application live sur {{site.data.keyword.Bluemix_notm}}, arrêtez-la. Vous éviterez des frais imprévus.
{: tip}  

## Etapes suivantes

* [Tutoriels](/docs/tutorials/index.html)
* [Exemples ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
