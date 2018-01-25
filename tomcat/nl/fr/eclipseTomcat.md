---

copyright:
  years: 2017
lastupdated: "2017-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Développement d'applications Tomcat avec IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}

Vous pouvez aussi utiliser {{site.data.keyword.eclipsetoolsfull}} comme moyen alternatif de développer et déployer des applications sur {{site.data.keyword.Bluemix}}. IBM Eclipse Tools fournit des plug-ins que vous pouvez installer dans un environnement Eclipse existant afin de faciliter son intégration avec {{site.data.keyword.Bluemix_notm}}.

Cette procédure suit les mêmes étapes générales que le [Tutoriel Initiation](getting-started.html) pour Liberty. En utilisant Eclipse, vous allez configurer un environnement de développement, déployer une application à la fois localement et sur le cloud et intégrer un service de base de données dans votre application.

## Avant de commencer
{: #prereqs}

Vous aurez besoin des comptes et outils suivants :
* [IBM Eclipse Tools for IBM Cloud ![External Link icon](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}
* [Eclipse IDE for Java EE Developers ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}

Si vous avez suivi le [Tutoriel Initiation](getting-started.md), vous avez peut-être déjà ces outils et comptes. Veillez également à ce
que ce qui soit installé et enregistré avant de démarrer :
* [Compte {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI (client de ligne de commande pour Cloud Foundry) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://git-scm.com/downloads){: new_window}
* [Maven ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat version 8.0.41 ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}

## Etape 1 : Cloner l'application exemple
{: #clone}

Commencez par cloner le référentiel GitHub contenant l'application exemple.
  ```bash
git clone https://github.com/IBM-Bluemix/get-started-tomcat
  ```
  {: pre}

## Etape 2 : Générer (compiler) le code source de votre application
{: #build_app}

Utilisez Maven pour construire votre code source et exécuter l'application résultante.

1. Sur la ligne de commande, placez-vous dans le répertoire où se trouve l'application exemple.

  ```
cd get-started-tomcat
  ```
  {: pre}

1. Utilisez Maven pour installer les dépendances et construire le fichier .war.

  ```
mvn clean install
  ```
  {: pre}

## Etape 3 : Préparer l'application pour le déploiement
{: #prepare}

Pour déployer sur {{site.data.keyword.Bluemix_notm}}, il peut être utile de créer un fichier manifest.yml. Ce fichier inclut des informations essentielles sur votre application, telles que son nom, la quantité de mémoire à allouer à chaque instance et la route. Pour vous éviter d'avoir à le créer, nous avons prévu un exemple de fichier manifest.yml dans le répertoire `get-started-java`.

Ouvrez le fichier manifest.yml et, dans le champ `name`, remplacez le nom `GetStartedJava` par celui de votre application, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

```
applications:
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/GetStartedTomcat.war
    buildpack: java_buildpack
```
{: codeblock}

Dans ce fichier manifest.yml, l'effet de **random-route: true** est de générer une route aléatoire pour votre application afin d'éviter qu'elle n'entre en conflit avec d'autres.  Au besoin, vous pouvez remplacer **random-route: true** par **host: myChosenHostName** et fournir un nom d'hôte de votre choix. [En savoir plus...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## Etape 4 : Déployer sur {{site.data.keyword.Bluemix_notm}}
{: #deploy}

Déployez votre application dans l'une des régions Bluemix suivantes. Pour une latence aussi faible que possible, choisissez la région la plus proche de vos utilisateurs.

|Région          |Point d'extrémité d'API                  |
|:---------------|:-------------------------------|
| Sud des Etats-Unis |https://api.ng.bluemix.net     |
| Royaume-Uni | https://api.eu-gb.bluemix.net  |
| Sydney         | https://api.au-syd.bluemix.net |
| Francfort     | https://api.eu-de.bluemix.net |

1. Définissez le point d'extrémité d'API en remplaçant `<API-endpoint>` par le point d'extrémité de votre région.
  ```
cf api <API-endpoint>
  ```
  {: pre}

1. Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}}.
  ```
cf login
  ```
  {: pre}

  Si vous ne pouvez pas vous connecter à l'aide des commandes `cf login` ou `bx login` car vous disposez d'un ID utilisateur fédéré, utilisez la commande `cf login --sso` ou la commande `bx login --sso` pour vous connecter avec votre ID de connexion unique (SSO). Voir [Connexion à l'aide d'un ID fédéré](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) pour en savoir plus.

## Etape 5 : Développer avec Eclipse
{: #eclipse}

1. Assurez-vous d'avoir [IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix).

2. Importez l'exemple `get-started-java` dans Eclipse en sélectionnant **Fichier > Importer > Maven > Projets Maven existants**.

3. Créez une définition de serveur Tomcat :
  - Dans la vue `Serveurs`, faites un clic droit et choisissez `Nouveau` -> `Serveur`.
  - Sélectionnez `Apache` -> `Serveur Tomcat version 8.0`.
  - Choisissez votre `tomcat-install-dir` (répertoire d'installation de Tomcat).
  - Continuez à dérouler l'assistant jusqu'à la fin en conservant les options par défaut.

4. Lancez votre application localement sur le serveur Apache :
  - Faites un clic droit sur l'exemple `GetStartedTomcat` et choisissez `Exécuter en tant que` -> `Exécuter sur le serveur`.
  - Localisez et sélectionnez le serveur Tomcat localhost et cliquez sur Terminer.
  - En quelques secondes, votre application doit être lancée sur http://localhost:8080/GetStartedTomcat/

5. Lancez votre application sur {{site.data.keyword.Bluemix_notm}} :
  - Faites un clic droit sur l'exemple `GetStartedTomcat` et choisissez `Exécuter en tant que` -> `Exécuter sur le serveur`.
  - Localisez et sélectionnez `{{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}}` et cliquez sur Terminer.
  - Un assistant vous guide à travers les options de déploiement. Veillez à choisir un `Nom` unique pour votre application.
  - En quelques minutes, votre application doit être lancée à l'URL que vous avez choisie.

Et voilà ! Vous venez de lancer votre code à la fois localement et sur le cloud !

## Etape 6 : Ajouter une base de données
{: #add_database}

Nous allons à présent ajouter une base de données {{site.data.keyword.cloudantfull}} à l'application et configurer cette dernière pour qu'elle puisse être exécutée localement et sur {{site.data.keyword.Bluemix_notm}}.

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} dans votre navigateur. Accédez au `Tableau de bord`. Sélectionnez votre application en cliquant sur son nom dans la colonne `Nom`.
2. Cliquez sur `Connexions`, puis sur `Connecter un nouveau`.
2. Dans la section `Données &  analyse`, sélectionnez `{{site.data.keyword.cloudant_short_notm}}` et `Créer` pour créer le service.
3. Sélectionnez `Reconstituer` lorsque vous y êtes invité. {{site.data.keyword.Bluemix_notm}} redémarre votre application et lui fournit les données d'identification pour l'accès à la base de données en utilisant la variable d'environnement `VCAP_SERVICES`. L'application n'a accès à cette variable d'environnement que lorsqu'elle fonctionne sur {{site.data.keyword.Bluemix_notm}}.

Les variables d'environnement vous permettent de séparer les paramètres de déploiement de votre code source. Par exemple, plutôt que de coder en dur le mot de passe d'accès à la base de données, vous pouvez le stocker dans une variable d'environnement et inclure une référence à celle-ci dans votre code source. [En savoir plus...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Etape 7 : Utiliser la base de données
{: #use_database}
Nous allons à présent mettre à jour votre code local pour le faire pointer sur cette base de données. Créons à cet effet un fichier de propriétés pour y stocker les identifiants d'accès aux services. Ce fichier ne sera utilisé QUE lorsque l'application est exécutée localement. Lors de son fonctionnement sur {{site.data.keyword.Bluemix_notm}}, elle obtiendra ces identifiants en lisant la variable d'environnement VCAP_SERVICES.

1. Dans Eclipse, ouvrez le fichier src/main/resources/cloudant.properties :
  ```
  cloudant_url=
  ```
  {: pre}

2. Dans votre navigateur, ouvrez l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}, sélectionnez votre application -> Connexions -> Cloudant -> Afficher les données d'identification

3. Copiez seulement la partie `url` des données d'identification et collez-la dans le champ `url` du fichier `cloudant.properties`, puis sauvegardez les changements.  Le résultat doit être similaire au suivant :
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```

4. Redémarrez le serveur Tomcat dans Eclipse à partir de la vue `Serveurs`.

  Dans votre navigateur, actualisez la vue de http://localhost:8080/GetStartedTomcat/. Chaque nom que vous entrez dans l'application sera ajouté à la base de données.

  Votre application locale et son instance {{site.data.keyword.Bluemix_notm}} partagent la même base de données.  Vous pouvez visualiser votre application {{site.data.keyword.Bluemix_notm}} en accédant à l'URL obtenue précédemment dans la sortie de la commande push.  Les noms que vous ajoutez depuis l'une ou l'autre version de l'application doivent apparaître dans les deux lorsque vous actualisez les navigateurs.

Si vous n'avez pas besoin de votre application live sur {{site.data.keyword.Bluemix_notm}}, arrêtez-la. Vous éviterez des frais imprévus.
{: tip}  
