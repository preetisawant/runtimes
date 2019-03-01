---

copyright:
  years: 2017, 2018
lastupdated: "2018-6-26"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Utilisation d'un service fourni par l'utilisateur avec Liberty dans {{site.data.keyword.cloud_notm}}
{: #using_user_provided}

Cloud Foundry fournit un mécanisme permettant de se connecter à et d'utiliser des services
qui ne sont pas nécessairement fournis par ou disponibles au sein de votre environnement {{site.data.keyword.Bluemix_notm}}.
Cette fonction constitue les [services fournis par l'utilisateur](https://docs.cloudfoundry.org/devguide/services/user-provided.html).

Le présent document implique que :
  * vous disposez d'un service disponible, 
  * vous pouvez obtenir des données d'identification pour ce service,
et décrit la procédure requise pour se connecter à et utiliser le service en question avec l'exemple d'application
Getting-Started-Liberty (initiation à Liberty)

Pour cette discussion, nous allons utiliser l'instance CloudantNoSQLDB comme exemple de service,
et créer un service fourni par l'utilisateur pour s'y connecter.

## Etape 1 : Envoyer par commande push de l'application Getting-Started 
{: #follow_getting_started}

Suivez les étapes du [tutoriel d'initiation](/docs/runtimes/liberty/getting-started.html) jusqu'à l'envoi par commande push
de l'application à {{site.data.keyword.Bluemix_notm}}. Arrêtez-vous avant la connexion à la base de données.

## Etape 2 : Créer une instance CloudantNoSQLDB 
{: #create_cloudantnosqldb}

Suivez les étapes du [tutoriel d'initiation](/docs/runtimes/liberty/getting-started.html) pour
créer une instance CloudantNoSqLDB. 

Utilisez l'option d'affichage des données d'identification pour copier les données depuis la base de données CloudandNoSQLDB. Sauvegardez ces données d'identification dans un fichier local, par exemple cloudant-creds.

## Etape 3 : Créer un service fourni par l'utilisateur
Pour utiliser l'application Getting-Started,
le nom du service fourni par l'utilisateur doit comporter
"cloudantNoSQLDB".  L'application Getting-Started effectue l'analyse syntaxique
de la variable des services VCAP et recherche un service fourni par l'utilisateur
avec un nom contenant "cloudantNoSQLDB".

        ibmcloud cf cups my-cloudantNoSQLDB-ups -p cloudant-creds

## Etape 4 : Lier le service fourni par l'utilisateur et reconstituer l'application
Liez le service fourni par l'utilisateur à l'application d'initiation.

        ibmcloud cf bs GettingStartedLiberty my-cloudantNoSQLDB-ups

        ibmcloud cf restage GettingStartedLiberty

## Etape 5 : Confirmer
Accédez à votre application et confirmez que vous pouvez
ajouter plusieurs noms à la zone 'name'.
