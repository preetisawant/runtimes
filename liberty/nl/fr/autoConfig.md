---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Configurer les services liés
{: #auto_config}

Vous pouvez lier divers services à votre application Liberty for Java. Les services peuvent être gérés par le conteneur, gérés par l'application, ou les deux, selon le souhait du développeur.

Un service géré par l'application est un service entièrement géré par l'application, sans aucune assistance de Liberty. L'application lit normalement la variable VCAP_SERVICES pour obtenir des informations sur le service lié et accède directement au service. L'application fournit tout le code d'accès client nécessaire. Il n'existe aucune dépendance par rapport aux fonctions Liberty ou à la configuration du fichier server.xml. La configuration automatique par le pack de construction Liberty ne s'applique pas aux services de ce type.

Un service géré par le conteneur est un service qui est géré par l'exécution Liberty. Dans certains cas, l'application peut rechercher le service lié dans JNDI, alors que dans d'autres cas, le service est utilisé directement par Liberty lui-même. Le pack de construction Liberty lit VCAP_SERVICES afin d'obtenir des informations sur les services liés. Pour chaque service géré par le conteneur, le pack de construction effectue trois opérations :

* Il génère des [variables cloud](optionsForPushing.html#accessing_info_of_bound_services) pour le service lié.
* Il installe les fonctions Liberty et les codes d'accès client requis pour permettre l'accès au service lié.
* Il génère ou met à jour les sections du fichier server.xml qui sont requises par le service.

Ce processus est dénommé configuration automatique.

Le pack de construction Liberty se charge de la configuration automatique des types de service suivants :

* [Auto-Scaling](/docs/services/Auto-Scaling/index.html#autoscaling)
* [Base de données ClearDB MySQL ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.cleardb.com/developers)
* [Cloudant NoSQL Database](/docs/services/Cloudant/index.html#Cloudant)
* [Compose for MongoDB](/docs/services/ComposeForMongoDB/index.html)
* [Compose for MySQL](/docs/services/ComposeForMySQL/index.html)
* [Compose for PostgreSQL](/docs/services/ComposeForPostgreSQL/index.html)
* [dashDB](/docs/services/dashDB/index.html#dashDB)
* [ElephantSQL](docs/services/ElephantSQL/index.html)
* [Single Sign On](/docs/services/SingleSignOn/index.html#sso_gettingstarted)

Les services Compose peuvent être gérés par le conteneur ou gérés par l'application. Par défaut, le pack de construction Liberty suppose que ces services sont gérés par le conteneur et les configure automatiquement. Si vous souhaitez que le service soit géré par l'application, vous pouvez résilier sa configuration automatique par Liberty en configurant la variable d'environnement `services_autoconfig_excludes`. Pour plus d'informations, voir [Résiliation de la configuration automatique des services](autoConfig.html#opting_out).

## Installation des fonctions Liberty et du code d'accès client
{: #installation_of_liberty_features}

Lorsque vous créez une liaison à un service géré par le conteneur, le service peut nécessiter une configuration de fonctions Liberty dans la section featureManager du fichier server.xml. Le pack de construction Liberty met à jour la section featureManager et installe les fichiers binaires de support requis. Si le service requiert des fichiers Jar de pilote client, ces fichiers Jar sont téléchargés à un emplacement prédéterminé dans le répertoire d'installation de
Liberty.

Voir la section [Résiliation de la configuration automatique des services](#opting_out) pour obtenir plus de détails sur les types de service lié.

## Génération ou mise à jour des sections de configuration dans le fichier server.xml
{: #generating_or_updating_serverxml}

Lorsque vous poussez une application autonome, en fonction de la manière dont elle est liée aux services et
selon que vous avez ou non un fichier server.xml existant, le pack de construction
Liberty peut générer automatiquement les sections de configuration ou mettre à jour des sections existantes.


Lorsque vous poussez une application autonome, le pack de construction Liberty génère, pour le fichier server.xml, la section de configuration appropriée, comme décrit dans la rubrique [Options pour l'envoi par commande push d'applications Liberty](optionsForPushing.html#options_for_pushing), sur {{site.data.keyword.Bluemix_notm}}. 

Lorsque vous envoyez une application autonome par commande push et que vous la liez à des services gérés par conteneur, le pack de construction Liberty génère les sections server.xml requises pour les services liés.

Lorsque vous fournissez un fichier server.xml et que vous créez une liaison avec des services gérés par le conteneur, le pack de construction Liberty génère les sections de configuration ou met à jour les sections existantes.

* Si le fichier server.xml fourni ne comporte pas de sections de configuration pour les services liés, Liberty les génère.
* Si le fichier server.xml fourni comporte déjà des sections de configuration pour les services liés, Liberty les met à jour.

Pour plus d'informations, consultez la documentation relative au type de service lié.

## Résiliation de la configuration automatique des services
{: #opting_out}

Dans certains cas, vous ne souhaiterez peut-être pas que le pack de construction Liberty configure automatiquement les services qui ont été liés. Considérez les scénarios suivants :

* Votre application utilise *dashDB*, mais vous souhaitez qu'elle gère directement la connexion à la base de données. L'application contient le fichier Jar de pilote client requis. Vous ne voulez
pas que le pack de construction Liberty configure automatiquement le service *dashDB*.

* Vous avez soumis un fichier server.xml comportant les sections de configuration pour l'instance *cloudant* car vous avez besoin d'une configuration de source de données non standard. Vous ne voulez pas que le pack de construction Liberty mette à jour le fichier server.xml, mais vous souhaitez tout de même qu'il vérifie que le logiciel de prise en charge est installé.

Pour résilier la configuration automatique des services, utilisez alors la variable d'environnement services_autoconfig_excludes. Vous pouvez inclure cette variable d'environnement dans un fichier manifest.yml ou la définir à l'aide du client cf.

Vous pouvez résilier la configuration automatique des services sur une base individuelle. Vous pouvez opter pour une résiliation complète (comme dans le scénario *dashDB*) ou
seulement des mises à jour du fichier de configuration
server.xml (comme
dans le scénario *cloudant*). La valeur que vous spécifiez pour la variable d'environnement services_autoconfig_excludes est une chaîne ayant les caractéristiques suivantes :

* La chaîne peut contenir des spécifications de résiliation pour un ou plusieurs services.
* La spécification de la résiliation pour un service donné est type_service=option, où :
  * type_service est le label du service tel que mentionné dans VCAP_SERVICES.
  * option est soit "all", soit "config" (sans les guillemets).
* Si la chaîne contient une spécification de résiliation pour plusieurs services, les spécifications individuelles doivent être séparées par un espace unique.

Examinez cet exemple de grammaire pour la chaîne services_autoconfig_excludes :

```
    Opt_out_string :: <spécification_type_service[<delimiter>spécification_type_service]*
    <spécification_type_service> :: <type_service>=<option>
    <type_service> :: type de service (label du service tel qu'il figure dans VCAP_SERVICES)
    <option> :: all | config
    <délimiteur> :: un seul espace
```
{: codeblock}

**Important** : Le type de service que vous indiquez doit correspondre au libellé des services tel qu'il figure dans la variable d'environnement VCAP_SERVICES. Le caractère espace n'est pas admis.
**Important** : Aucun espace n'est autorisé dans une entrée ```<spécification_type_service>```. L'unique utilisation admise d'un espace est pour
la séparation de plusieurs instances de ```<spécification_type_service>```.

Utilisez l'option **all** pour résilier toutes les actions de configuration automatique d'un service donné, comme dans le scénario *dashDB* ci-dessus. Utilisez l'option **config**
pour résilier uniquement les actions de mise à jour
de la configuration, comme dans le scénario *cloudant* ci-dessus.


Voici quelques exemples de résiliation de configuration automatique dans un fichier manifest.yml pour les scénarios *dashDB* et *cloudant*.

```
    env:
      services_autoconfig_excludes: dashDB=all

    env:
      services_autoconfig_excludes: cloudant=config

    env:
      services_autoconfig_excludes: cloudant=config dashDB=all
```
{: codeblock}

Ci-dessous figurent des exemples de définition de la variable d'environnement services_autoconfig_excludes pour l'application myapp à l'aide de l'interface de ligne de commande.

```
    cf set-env myapp services_autoconfig_excludes cloudant=config
    cf set-env myapp services_autoconfig_excludes "cloudant=config dashDB=all"
```
{: codeblock}

Pour trouver le *label* d'un service dans VCAP_SERVICES, émettez une commande comme celle de l'exemple suivant : 

```
    cf env myapp
```
{: codeblock}

La sortie inclut un texte similaire au suivant, dans lequel vous pouvez voir le champ **label** avec la valeur **elephantsql** :

```
   "elephantsql": [
   {
      "credentials": {
      "max_conns": "5",
      "uri":      "..."
   },
   "label": "elephantsql",

```
{: codeblock}

## Remplacement de la configuration du service
{: #override_service_config}

Dans certains cas, il est souhaitable d'outrepasser la configuration par défaut générée automatiquement pour un service.
Vous pouvez à cet effet utiliser la variable d'environnement
**LBP_SERVICE_CONFIG_xxxx**.
Référez-vous aux tableaux suivants pour obtenir le nom complet de chaque variable
d'environnement et un exemple de syntaxe permettant d'outrepasser la configuration
automatique du service correspondant.
Par exemple,
pour outrepasser la version par défaut du service *elephantSQL* et forcer l'utilisation de la version 8.3.4.+ à la place, émettez une commande telle que :


```
    cf set-env myapp LBP_SERVICE_CONFIG_POSTGRESQL "{driver: { version: 8.3.4.+ }}"
```
{: codeblock}

Ce tableau indique la correspondance entre **type_service** et nom de variable d'environnement **LBP_SERVICE_CONFIG_xxxx**.

<table>
<tr>
<th align="left">type_service</th>
<th align="left">Nom de la variable d'environnement</th>
</tr>

<tr>
<td>Auto-Scaling</td>
<td>LBP_SERVICE_CONFIG_AUTO-SCALING</td>
</tr>

<tr>
<td>cleardb</td>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
</tr>

<tr>
<td>cloudantNoSQLDB</td>
<td>LBP_SERVICE_CONFIG_CLOUDANTNOSQLDB</td>
</tr>

<tr>
<td>compose-for-mongodb</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MONGO</td>
</tr>

<tr>
<td>compose-for-mysql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
</tr>

<tr>
<td>compose-for-postgresql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
</tr>

<tr>
<td>elephantsql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
</tr>

<tr>
<td>SingleSignOn</td>
<td>LBP_SERVICE_CONFIG_SINGLESIGNON</td>
</tr>
</table>


Le tableau suivant indique la syntaxe permettant de remplacer certaines options de configuration de service :

<table>
<tr>
<th align="left">Nom de la variable d'environnement</th>
<th align="left">Syntaxe de la configuration</th>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>
</table>



# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
