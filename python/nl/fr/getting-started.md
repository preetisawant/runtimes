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
{: #getting_started}

* {: download} Félicitations, vous avez déployé une application exemple Hello World sur {{site.data.keyword.Bluemix}} !  Pour commencer, suivez ce guide pas à pas. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Télécharger l'exemple de code)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Télécharger le code de l'application" />téléchargez l'exemple de code</a> et découvrez-le par vous-même.

En suivant ce tutoriel d'initiation Python, vous allez configurer un environnement de développement, déployer une application localement et sur {{site.data.keyword.Bluemix}}, puis intégrer un service de base de données dans votre application.

## Avant de commencer
{: #prereqs}

Vous aurez besoin des éléments suivants :
* [Compte {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI (client de ligne de commande pour Cloud Foundry) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://git-scm.com/downloads){: new_window}
* [Python ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.python.org/downloads/){: new_window}

## Etape 1 : Cloner l'application exemple
{: #clone}

Vous êtes maintenant prêt à travailler avec l'application. Clonez le référentiel et placez-vous dans le répertoire où se trouve l'application exemple.
  ```
git clone https://github.com/IBM-Bluemix/get-started-python
  ```
  {: pre}
  ```
cd get-started-python
  ```
  {: pre}

  Examinez attentivement les fichiers dans le répertoire *get-started-python* afin de vous familiariser avec leur contenu.

## Etape 2 : Exécuter l'application localement
{: #run_locally}

Voir [The Hitchhiker’s Guide to Python! ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://docs.python-guide.org/en/latest/) pour obtenir de l'aide sur la configuration de Python sur votre système.
{: tip}

Installez les dépendances listées dans le fichier [requirements.txt![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://pip.readthedocs.io/en/stable/user_guide/#requirements-files) afin de pouvoir exécuter l'application localement.

Au besoin, vous pouvez utiliser un [environnement virtuel ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://packaging.python.org/installing/#creating-and-using-virtual-environments) pour éviter toute contradiction entre ces dépendances et celles d'autres projets Python ou de votre système d'exploitation.

  ```
pip install -r requirements.txt
  ```
  {: pre}

Avec Python3, vous pouvez également émettre la commande

  ```
python3 -m pip install -r requirements.txt
  ```
  {: pre}

Exécutez l'application.
  ```
python hello.py
  ```
  {: pre}

 Affichez votre application sur : http://localhost:8000


## Etape 3 : Préparer l'application pour le déploiement
{: #prepare}

Pour déployer sur {{site.data.keyword.Bluemix_notm}}, il peut être utile de créer un fichier manifest.yml. Ce fichier inclut des informations essentielles sur votre application, telles que son nom, la quantité de mémoire à allouer à chaque instance et la route. Pour vous éviter d'avoir à le créer, nous avons prévu un exemple de fichier manifest.yml dans le répertoire `get-started-python`.

Ouvrez le fichier manifest.yml et, dans le champ `name`, remplacez le nom `GetStartedPython` par celui de votre application, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
  - name: GetStartedPython
    random-route: true
    memory: 128M
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

Connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}}.

  ```
cf login
  ```
  {: pre}

Si vous ne pouvez pas vous connecter à l'aide des commandes `cf login` ou `bx login` car vous disposez d'un ID utilisateur fédéré, utilisez la commande `cf login --sso` ou la commande `bx login --sso` pour vous connecter avec votre ID de connexion unique (SSO). Voir [Connexion à l'aide d'un ID fédéré](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) pour en savoir plus.

Depuis le répertoire *get-started-python*, poussez votre application vers {{site.data.keyword.Bluemix_notm}}
  ```
cf push
  ```
  {: pre}

Cette opération peut prendre une minute. En cas d'erreur dans le processus de déploiement, vous pouvez utiliser la commande `cf logs <Your-App-Name> --recent` pour identifier et résoudre le problème.

Une fois le déploiement achevé, vous devez voir un message indiquant que votre application est lancée.  Vous pouvez visualiser l'application en accédant à l'URL qui figure dans la sortie de la commande push.  Vous pouvez aussi émettre la commande
  ```
cf apps
  ```
  {: pre}
  pour voir l'état de votre application et obtenir son URL.

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

1. Créez un fichier nommé `vcap-local.json` dans le répertoire `get-started-python` et ajoutez-y le contenu suivant :
  ```
  {
    "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "username":"CLOUDANT_DATABASE_USERNAME",
            "password":"CLOUDANT_DATABASE_PASSWORD",
            "host":"CLOUDANT_DATABASE_HOST"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
    }
  }
  ```
  {: pre}

2. De retour dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}, sélectionnez votre application -> Connexions -> Cloudant -> Afficher les données d'identification

3. Copiez les valeurs des champs `username`, `password` et `host` des données d'identification dans les mêmes champs du fichier `vcap-local.json`, en remplaçant **CLOUDANT_DATABASE_USERNAME**, **CLOUDANT_DATABASE_PASSWORD** et **CLOUDANT_DATABASE_URL**.

4. Lancez votre application localement.
  ```
python hello.py
  ```
  {: pre}

  Affichez votre application sur : http://localhost:8000. Chaque nom que vous entrez dans l'application sera ajouté à la base de données.

  Votre application locale et son instance {{site.data.keyword.Bluemix_notm}} partagent la même base de données.  Vous pouvez visualiser votre application {{site.data.keyword.Bluemix_notm}} en accédant à l'URL obtenue précédemment dans la sortie de la commande push.  Les noms que vous ajoutez depuis l'une ou l'autre version de l'application doivent apparaître dans les deux lorsque vous actualisez les navigateurs.

Si vous n'avez pas besoin de votre application live, arrêtez-la. Vous éviterez des frais imprévus.
{: tip}

## Etapes suivantes

* [Tutoriels](/docs/tutorials/index.html)
* [Exemples ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
