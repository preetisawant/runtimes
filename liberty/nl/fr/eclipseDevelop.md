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

# Développement d'applications avec IBM Eclipse Tools for {{site.data.keyword.cloud_notm}}

Vous pouvez aussi utiliser {{site.data.keyword.eclipsetoolsfull}} comme moyen alternatif de développer et déployer des applications sur {{site.data.keyword.Bluemix}}. {{site.data.keyword.eclipsetoolsfull}} fournit des plug-ins que vous pouvez installer dans un environnement Eclipse existant afin de faciliter son intégration avec {{site.data.keyword.Bluemix_notm}}.

Cette procédure suit les mêmes étapes générales que le [Tutoriel Initiation](getting-started.html) pour Liberty. En utilisant Eclipse, vous allez configurer un environnement de développement, déployer une application à la fois localement et sur le cloud et intégrer un service de base de données {{site.data.keyword.Bluemix_notm}} dans votre application.

## Avant de commencer
{: #prereqs}

Vous aurez besoin des comptes et outils suivants :
* [IBM Eclipse Tools for IBM Cloud ![External Link icon](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}
* [Eclipse IDE for Java EE Developers ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}

Si vous avez suivi le [Tutoriel Initiation](getting-started.md), vous avez peut-être déjà ces outils et comptes. Veillez également à ce que ce qui soit installé et enregistré avant de démarrer :
* [Compte {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [Interface CLI {{site.data.keyword.Bluemix_notm}}](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://git-scm.com/downloads){: new_window}
* [Maven ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://maven.apache.org/download.cgi){: new_window}

## Etape 1 : Cloner l'application exemple
{: #clone}

Commencez par cloner le référentiel GitHub contenant l'application exemple.

  ```
git clone https://github.com/IBM-Cloud/get-started-java
  ```
  {: codeblock}

## Etape 2 : Générer (compiler) le code source de votre application
{: #build_app}

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

## Etape 4 : Se connecter à {{site.data.keyword.Bluemix_notm}}
{: #deploy}

1. Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}} et sélectionnez un point de terminaison d'API.

  ```
ibmcloud login
  ```
  {: codeblock}

  Si vous ne pouvez pas vous connecter via `ibmcloud login` car vous possédez un ID utilisateur fédéré, utilisez la commande suivante pour vous connecter à l'aide de votre ID de connexion unique. Voir [Connexion à l'aide d'un ID fédéré](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) pour en savoir plus.

  ```
ibmcloud login --sso
  ```
  {: codeblock}

  Accédez ensuite à l'interface CLI Cloud Foundry :

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Si vous ne disposez pas d'une organisation ou d'un espace configuré, voir [Ajout d'organisations et d'espaces](https://console.bluemix.net/docs/account/orgs_spaces.html).
  {: tip}

## Etape 5 : Développer avec Eclipse
{: #eclipse}

1. Assurez-vous d'avoir [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix).

2. Importez l'exemple `get-started-java` dans Eclipse en sélectionnant **Fichier > Importer > Maven > Projets Maven existants**.

3. Créez une définition de serveur Liberty. Les étapes suivantes permettent de télécharger un nouveau serveur Liberty.
  - Dans la vue **Fenêtre > Afficher la vue > Serveurs**, faites un clic droit et sélectionnez **Nouveau > Serveur**.
  - Sélectionnez **IBM > WebSphere Application Server Liberty**.
  - Sélectionnez **Installer depuis une archive ou un référentiel**.
  - Lorsque vous y êtes invité, entrez le chemin menant au nouveau dossier (/Users/username/liberty) dans lequel vous voulez installer Liberty.
  - Sélectionnez **Télécharger et installer un nouvel environnement d'exécution à partir d'ibm.com**.
  - Sélectionnez **WAS Liberty avec profil Web Java EE 7**.
  - Continuez à dérouler l'assistant jusqu'à la fin en conservant les options par défaut.

4. Lancez votre application localement sur Liberty :
  - Changez le navigateur web de l'environnement pour le navigateur par défaut du système en sélectionnant **Fenêtre > Navigateur web > Navigateur Web système par défaut**.
  - Faites un clic droit sur l'exemple `GetStartedJava` et choisissez **Exécuter en tant que > Exécuter sur le serveur**.
  - Localisez et sélectionnez le serveur Liberty localhost et cliquez sur **Terminer**.

  En quelques secondes, votre application doit être lancée sur http://localhost:9080/GetStartedJava.

5. Modifiez le code :
  - Ouvrez `src/main/webapp/index.html` et remplacez le titre `<h1>Bienvenue.</h1>` par `<h1>Bienvenue Jane.</h1>`.
  - Enregistrez vos changements. Ils sont pris en compte automatiquement par Liberty.
  - Actualisez votre navigateur (http://localhost:9080/GetStartedJava) pour voir vos changements.

6. Envoyez vos changements par commande push vers {{site.data.keyword.Bluemix_notm}} :
  - Sur la ligne de commande, à partir du répertoire `get-started-java`, reconstruisez le fichier .war.

    ```
mvn clean install
    ```
    {: codeblock}

  - Envoyez votre application par commande push vers {{site.data.keyword.Bluemix_notm}}.

    ```
ibmcloud cf push
    ```
    {: codeblock}

Et voilà ! Vous venez de lancer votre code à la fois localement et sur le cloud !

## Etape 6 : Ajouter une base de données
{: #add_database}

Nous allons à présent ajouter une base de données NoSQL à l'application et configurer cette dernière pour qu'elle puisse être exécutée localement et sur {{site.data.keyword.Bluemix_notm}}.

1. Dans votre navigateur, connectez-vous à {{site.data.keyword.Bluemix_notm}} et allez au Tableau de bord. Sélectionnez **Créer une ressource**.
2. Choisissez la section **Données et analyse**, puis sélectionnez **{{site.data.keyword.cloudant_short_notm}}** et créez votre service.
3. Accédez à la vue **Connexions** et sélectionnez votre application, puis **Créer une connexion**.
4. Sélectionnez **Reconstituer** lorsque vous y êtes invité. {{site.data.keyword.Bluemix_notm}} redémarre votre application et lui fournit les données d'identification pour l'accès à la base de données en utilisant la variable d'environnement `VCAP_SERVICES`. L'application n'a accès à cette variable d'environnement que lorsqu'elle fonctionne sur {{site.data.keyword.Bluemix_notm}}.

Les variables d'environnement vous permettent de séparer les paramètres de déploiement de votre code source. Par exemple, plutôt que de coder en dur le mot de passe d'accès à la base de données, vous pouvez le stocker dans une variable d'environnement et inclure une référence à celle-ci dans votre code source.
{: tip}

## Etape 7 : Utiliser la base de données
{: #use_database}
Nous allons à présent mettre à jour votre code local pour le faire pointer sur cette base de données. Créons à cet effet un fichier de propriétés pour y stocker les identifiants d'accès aux services. Ce fichier ne sera utilisé QUE lorsque l'application est exécutée localement. Lors de son fonctionnement sur {{site.data.keyword.Bluemix_notm}}, elle obtiendra ces identifiants en lisant la variable d'environnement `VCAP_SERVICES`.

1. Dans Eclipse, ouvrez le fichier src/main/resources/cloudant.properties :

  ```
  cloudant_url=
  ```
  {: codeblock}

2. Dans votre navigateur, accédez à {{site.data.keyword.Bluemix_notm}} et sélectionnez **Applications > _votre application_ > Connexions > Cloudant > Afficher les données d'identification**.

3. Copiez seulement la partie `url` des données d'identification et collez-la dans le champ `url` du fichier `cloudant.properties`, puis sauvegardez les changements.

  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:codeblock}

4. Redémarrez le serveur Liberty dans Eclipse à partir de la vue `Serveurs`.

  Dans votre navigateur, actualisez la vue de http://localhost:9080/GetStartedJava/. Chaque nom que vous entrez dans l'application sera ajouté à la base de données.

  Votre application locale et son instance {{site.data.keyword.Bluemix_notm}} partagent la même base de données. Les noms que vous ajoutez depuis l'une ou l'autre version de l'application doivent apparaître dans les deux lorsque vous actualisez les navigateurs.


Si vous n'avez pas besoin de votre application live sur {{site.data.keyword.Bluemix_notm}}, arrêtez-la. Vous éviterez des frais imprévus.
{: tip}  
