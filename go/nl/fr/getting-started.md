---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-24"

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

En suivant ce tutoriel d'initiation, vous allez configurer un environnement de développement, déployer une application localement et sur {{site.data.keyword.Bluemix}}, puis intégrer un service de base de données {{site.data.keyword.Bluemix_notm}} dans votre application.

Tout au long de ces documents, les références à l'interface CLI Cloud Foundry sont désormais mis à jour dans l'interface CLI de {{site.data.keyword.Bluemix_notm}}. L'interface CLI {{site.data.keyword.Bluemix_notm}} possède les mêmes commandes Cloud Foundry familières, mais avec une meilleure intégration aux comptes et autres services {{site.data.keyword.Bluemix_notm}}. Ce tutoriel vous permet d'en apprendre davantage sur l'initiation à l'interface CLI {{site.data.keyword.Bluemix_notm}}.
{: tip}

## Avant de commencer
{: #prereqs}

Vous aurez besoin des éléments suivants :
* [Compte {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [Interface CLI {{site.data.keyword.Bluemix_notm}}](../../cli/reference/ibmcloud/download_cli.html)
* [Git ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://git-scm.com/downloads){: new_window}
* [Go ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://golang.org/dl/){: new_window}

## Etape 1 : Cloner l'application exemple
{: #clone}

1. Vous allez d'abord mettre en place l'environnement local en veillant à configurer correctement toutes les variables d'environnement GO. Par exemple :

  ```
mkdir $HOME/work
export GOPATH=$HOME/work
export PATH=$PATH:$GOPATH/bin
  ```
  {: codeblock}

1. Passez dans le chemin $GOPATH/src

  ```
mkdir $GOPATH/src
cd $GOPATH/src
  ```
  {: codeblock}

  Vous êtes maintenant prêt à utiliser l'application Go *hello world*.
1. Clonez le référentiel et placez-vous dans le répertoire où se trouve l'application exemple.

  ```
go get github.com/IBM-Cloud/get-started-go
  ```
  {: codeblock}

  ```
cd github.com/IBM-Cloud/get-started-go
  ```
  {: codeblock}

1. Examinez attentivement les fichiers dans le répertoire **`get-started-go`** afin de vous familiariser avec leur contenu.

## Etape 2 : Exécuter l'application localement
{: #run_locally}

1. Générez et exécutez l'application en local en exécutant les commandes suivantes.

  ```
make
  ```
  {: codeblock}

  ```
go run main.go
  ```
  {: pre}

1. Affichez votre application sur l'URL suivante : http://localhost:8080

Appuyez sur *Ctrl-C* pour arrêter votre application depuis la même fenêtre que celle d'où vous l'avez lancée.
{: tip}

## Etape 3 : Préparer l'application pour le déploiement
{: #prepare}

Pour déployer sur {{site.data.keyword.Bluemix_notm}}, il peut être utile de créer un fichier manifest.yml. Ce fichier inclut des informations essentielles sur votre application, telles que son nom, la quantité de mémoire à allouer à chaque instance et la route. Pour vous éviter d'avoir à le créer, nous avons prévu un exemple de fichier manifest.yml dans le répertoire `get-started-go`.

Ouvrez le fichier manifest.yml et, dans le champ `name`, remplacez le nom `GetStartedGo` par celui de votre application, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedGo
   random-route: true
   memory: 128M
   buildpack: go_buildpack
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

1. Depuis le répertoire **`get-started-go`**, envoyez votre application par commande push vers {{site.data.keyword.Bluemix_notm}}

  ```
ibmcloud cf push
  ```
  {: codeblock}

  Cette opération peut prendre une minute. En cas d'erreur dans le processus de déploiement, vous pouvez utiliser la commande `ibmcloud cf logs <Your-App-Name> --recent` pour identifier et résoudre le problème.

Une fois le déploiement achevé, vous devez voir un message indiquant que votre application est lancée.  Vous pouvez visualiser l'application en accédant à l'URL qui figure dans la sortie de la commande push. Vous pouvez aussi émettre la commande suivante pour voir l'état de votre application et obtenir son URL.

  ```
ibmcloud cf apps
  ```
  {: codeblock}

## Etape 5 : Ajouter une base de données
{: #add_database}

Nous allons à présent ajouter une base de données {{site.data.keyword.cloudant_short_notm}} NoSQL à l'application et configurer cette dernière pour qu'elle puisse être exécutée localement et sur {{site.data.keyword.Bluemix_notm}}.

1. Dans votre navigateur, connectez-vous à {{site.data.keyword.Bluemix_notm}} et allez au Tableau de bord. Sélectionnez **Créer une ressource**.
1. Recherchez **{{site.data.keyword.cloudant_short_notm}}** puis sélectionnez le service.
1. Pour les **méthodes d'authentification disponibles**, sélectionnez **Utiliser les données d'identification existantes et IAM**. Vous pouvez conserver les paramètres par défaut pour les autres zones. Cliquez sur **Créer** pour créer le service.
1. Dans la zone de navigation, accédez à **Connexions**. Sélectionnez votre application, puis cliquez sur **Créer une connexion**.
1. Connectez-vous à votre application en utilisant les valeurs par défaut, puis cliquez sur **Connecter et reconstituer l'application**. Cliquez ensuite sur **Reconstituer** lorsque vous y êtes invité. 

   {{site.data.keyword.Bluemix_notm}} redémarre votre application et lui fournit les données d'identification pour l'accès à la base de données en utilisant la variable d'environnement `VCAP_SERVICES`. L'application n'a accès à cette variable d'environnement que lorsqu'elle fonctionne sur {{site.data.keyword.Bluemix_notm}}.

Les variables d'environnement vous permettent de séparer les paramètres de déploiement de votre code source. Par exemple, au lieu de coder en dur un mot de passe de base de données, vous pouvez le stocker dans une variable d'environnement que vous référencez dans votre code source.
{: tip}

## Etape 6 : Utiliser la base de données
{: #use_database}
Nous allons à présent mettre à jour votre code local pour le faire pointer sur cette base de données. Créons à cet effet un fichier .env pour y stocker les identifiants d'accès aux services que l'application utilisera. Ce fichier ne sera utilisé QUE lorsque l'application est exécutée localement. Lors de son fonctionnement sur {{site.data.keyword.Bluemix_notm}}, elle obtiendra ces identifiants en lisant la variable d'environnement VCAP_SERVICES.

1. Créez un fichier nommé `.env` dans le répertoire `get-started-go` et ajoutez-y le contenu suivant :

  ```
CLOUDANT_URL=
  ```
  {: codeblock}

2. Dans votre navigateur, accédez au tableau de bord {{site.data.keyword.Bluemix_notm}} et sélectionnez **_votre appli_ > Connexions**. Cliquez sur l'icône de menu {{site.data.keyword.cloudant_short_notm}} (**&vellip;**) et sélectionnez **Afficher les données d'identification**.

3. Copiez seulement la partie `url` des données d'identification et collez-la dans le champ `CLOUDANT_URL` du fichier `.env`, puis sauvegardez les changements.  Le résultat doit être similaire au suivant :

  ```
CLOUDANT_URL=https://123456789 ... bluemix.cloudant.com
  ```
  {: codeblock}

4. Lancez votre application localement.

  ```
go run main.go
  ```
  {: codeblock}

  Affichez votre application sur : http://localhost:8080. Chaque nom que vous entrez dans l'application sera ajouté à la base de données.

Votre application locale et son instance {{site.data.keyword.Bluemix_notm}} partagent la même base de données.  Vous pouvez visualiser votre application {{site.data.keyword.Bluemix_notm}} en accédant à l'URL obtenue précédemment dans la sortie de la commande push.  Les noms que vous ajoutez depuis l'une ou l'autre version de l'application doivent apparaître dans les deux lorsque vous actualisez les navigateurs.


Si vous n'avez pas besoin de votre application live, arrêtez-la. Vous éviterez des frais imprévus.
{: tip}

## Etapes suivantes

* [Tutoriels](/docs/tutorials/index.html)
* [Exemples ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
