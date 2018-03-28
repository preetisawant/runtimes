---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-14"

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

## Avant de commencer
{: #prereqs}
* [Git ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://git-scm.com/downloads){: new_window}
* [Cloud Foundry CLI (client de ligne de commande pour Cloud Foundry) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Compilateur Swift ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://swift.org/download/) pour votre plateforme.

## Etape 1 : Cloner l'application exemple
{: #clone}

Vous êtes maintenant prêt à travailler avec l'application Swift. Clonez le référentiel et placez-vous dans le répertoire où se trouve l'application exemple.
  ```
git clone https://github.com/IBM-Bluemix/get-started-swift
  ```
  {: pre}

  ```
cd get-started-swift
  ```
  {: pre}

  Examinez attentivement les fichiers dans le répertoire *get-started-swift* afin de vous familiariser avec leur contenu.

## Etape 2 : Exécuter l'application localement
{: #run_locally}

Ayant installé le compilateur Swift et cloné ce référentiel Git, vous pouvez à présent compiler et exécuter l'application. Accédez au répertoire racine de ce référentiel sur votre système et émettez la commande suivante :
```
swift build
```
{: pre}

Cette commande peut prendre quelques minutes pour s'exécuter.

Une fois l'application correctement compilée, vous pouvez lancer l'exécutable qui a été généré par le compilateur Swift :
```
.build/debug/get-started-swift
```
{: pre}

Vous devriez obtenir un résultat semblable au suivant :

```
Server is listening on port: 8080
```
{: codeblock}

Affichez votre application sur : http://localhost:8080

## Etape 3 : Préparer l'application pour le déploiement
{: #prepare}

Pour déployer sur {{site.data.keyword.Bluemix_notm}}, il peut être utile de créer un fichier manifest.yml. Ce fichier inclut des informations essentielles sur votre application, telles que son nom, la quantité de mémoire à allouer à chaque instance et la route. Pour vous éviter d'avoir à le créer, nous avons prévu un exemple de fichier manifest.yml dans le répertoire `get-started-swift`.

Ouvrez le fichier manifest.yml et, dans le champ `name`, remplacez le nom `GetStartedSwift` par celui de votre application, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedSwift
     random-route: true
     memory: 256M
     command: kitura-helloworld
     buildpack: swift_buildpack
  ```
  {: codeblock}

Dans ce fichier manifest.yml, l'effet de **random-route: true** est de générer une route aléatoire pour votre application afin d'éviter qu'elle n'entre en conflit avec d'autres.  Au besoin, vous pouvez remplacer **random-route: true** par **host: myChosenHostName** et fournir un nom d'hôte de votre choix. [En savoir plus...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## Etape 4 : Déployer l'application
{: #deploy}

Vous pouvez utiliser l'interface de ligne de commande Cloud Foundry pour déployer des applications.

Choisissez votre point d'extrémité d'API
  ```
cf api <API-endpoint>
  ```
  {: pre}

Dans cette commande, remplacez *API-endpoint* par un point d'extrémité d'API parmi les suivants.

| **Nom de région** | **Emplacement géographique** | **Point d'extrémité d'API** |
|-----------------|-------------------------|-------------------|
| Région Sud des Etats-Unis | Dallas, US | api.ng.bluemix.net |
| Région Est des Etats-Unis | Washington, DC, US | api.us-east.bluemix.net |
| Région Royaume-Uni | Londres, Angleterre | api.eu-gb.bluemix.net |
| Région Sydney | Sydney, Australie | api.au-syd.bluemix.net |
| Région Allemagne | Francfort, Allemagne | api.eu-de.bluemix.net |
{: caption="Tableau 1. Liste des régions {{site.data.keyword.cloud_notm}}" caption-side="top"}

Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}}

   ```
 cf login
   ```
   {: pre}

Si vous ne pouvez pas vous connecter à l'aide des commandes `cf login` ou `bx login` car vous disposez d'un ID utilisateur fédéré, utilisez la commande `cf login --sso` ou la commande `bx login --sso` pour vous connecter avec votre ID de connexion unique (SSO). Voir [Connexion à l'aide d'un ID fédéré](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) pour en savoir plus.

Depuis le répertoire *get-started-swift*, poussez votre application vers {{site.data.keyword.Bluemix_notm}}
   ```
 cf push
   ```
   {: pre}

Cette opération peut prendre une minute. En cas d'erreur dans le processus de déploiement, vous pouvez utiliser la commande `cf logs <Your-App-Name> --recent` pour identifier et résoudre le problème.

Une fois le déploiement achevé, vous devez voir un message indiquant que votre application est lancée.  Vous pouvez visualiser l'application en accédant à l'URL qui figure dans la sortie de la commande push.  Vous pouvez aussi émettre la commande `cf apps` pour voir l'état de votre application et obtenir son URL.

## Etape 5 : Ajouter une base de données
{: #add_database}

Nous allons à présent ajouter une base de données NoSQL à l'application et configurer cette dernière pour qu'elle puisse être exécutée localement et sur {{site.data.keyword.Bluemix_notm}}.

1. Dans votre navigateur, connectez-vous à {{site.data.keyword.Bluemix_notm}} et allez au Tableau de bord. Sélectionnez **Créer une ressource**.
2. Choisissez la section **Données et analyse**, puis sélectionnez **Cloudant NoSQL DB** et créez votre service.
3. Accédez à la vue **Connexions** et sélectionnez votre application, puis **Créer une connexion**.
4. Sélectionnez **Reconstituer** lorsque vous y êtes invité. {{site.data.keyword.Bluemix_notm}} redémarre votre application et lui fournit les données d'identification pour l'accès à la base de données en utilisant la variable d'environnement `VCAP_SERVICES`. L'application n'a accès à cette variable d'environnement que lorsqu'elle fonctionne sur {{site.data.keyword.Bluemix_notm}}.

Les variables d'environnement vous permettent de séparer les paramètres de déploiement de votre code source. Par exemple, plutôt que de coder en dur le mot de passe d'accès à la base de données, vous pouvez le stocker dans une variable d'environnement et inclure une référence à celle-ci dans votre code source. [En savoir plus...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Etape 6 : Utiliser la base de données
{: #use_database}

Nous allons à présent mettre à jour votre code local pour le faire pointer sur cette base de données. Créons à cet effet un fichier json pour y stocker les identifiants d'accès aux services que l'application utilisera. Ce fichier ne sera utilisé QUE lorsque l'application est exécutée localement. Lors de son fonctionnement sur {{site.data.keyword.Bluemix_notm}}, elle obtiendra ces identifiants en lisant la variable d'environnement VCAP_SERVICES.

Créez un fichier nommé `my-cloudant-credentials.json` dans le répertoire `config` et ajoutez-y le contenu suivant (référez-vous à `config/my-cloudant-credentials.json.example`) :

 ```
 {
   "password": "<password>",
   "url": "<url>",
   "username": "<username>"
 }
 ```

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

Cette application exemple utilise le package `CloudEnvironment` pour interagir avec {{site.data.keyword.Bluemix_notm}} en vue d'interpréter les variables d'environnement. [En savoir plus...](https://packagecatalog.com/package/IBM-Swift/CloudEnvironment)

L'emplacement réservé `cloudant`, dans la configuration `cloudfoundry:cloudant`,
facilite l'association d'un service Cloudant fourni par l'utilisateur à votre application. Avec la configuration `cloudfoundry:cloudant`, vous pouvez créer un service
Cloudant incluant la chaîne `cloudant` quelque part dans son nom et l'associer
à votre application sans avoir besoin d'éditer le fichier `config.json`. Si vous modifiez cette configuration et que vous souhaitez plus tard utiliser un service Cloudant fourni par vous-même,
vous devrez soit éditer la configuration pour y inclure `cloudfoundry:cloudant`, soit
définir `cloudfoundry:` avec le nom de votre service.
{: tip}

De retour dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}, sélectionnez votre application -> Connexions -> Cloudant -> Afficher les données d'identification

Copiez les données d'identification (et seulement elles) et collez-les dans les champs correspondants de votre fichier config.json local.

Construisez et lancez votre application localement.
 ```
swift build  
 ```
 {: pre}

  ```
.build/debug/kitura-helloworld
 ```
 {: pre}

Affichez votre application sur : http://localhost:8080. Chaque nom que vous entrez dans l'application sera ajouté à la base de données.

 Cette application exemple utilise le package `Kitura-CouchDB` pour interagir avec Cloudant. [En savoir plus...](https://packagecatalog.com/package/IBM-Swift/Kitura-CouchDB)

 Apportez les changements voulus et redéployez sur {{site.data.keyword.Bluemix_notm}}!

 ```
 cf app push
 ```

 Vous pouvez visualiser l'application en accédant à l'URL qui figure dans la sortie de la commande push. Par exemple, *myUrl.mybluemix.net*.

Si vous n'avez pas besoin de votre application live, arrêtez-la. Vous éviterez des frais imprévus.
{: tip}

## Etapes suivantes

* [Tutoriels](/docs/tutorials/index.html)
* [Exemples ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
