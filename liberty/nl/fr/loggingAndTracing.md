---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Configuration des fonctions de journalisation et de traçage
{: #logging_tracing}

## Fichiers journaux
{: #log_files}

Les journaux Liberty standard, tels que le fichier `messages.log` ou le répertoire `ffdc`, sont disponibles dans IBM Bluemix, dans le répertoire `logs` de chaque instance d'application. Vous pouvez accéder à ces journaux à partir de la console IBM Bluemix ou à via le client de ligne de commande pour Cloud Foundry. Par exemple :

* Pour accéder aux journaux récents d'une application, exécutez la commande suivante :

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* Pour voir le fichier `messages.log` d'une application lancée sur un noeud DEA, exécutez la commande suivante :

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* Pour voir le fichier `messages.log` d'une application lancée sur une cellule Diego, exécutez la commande suivante :

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

Vous
pouvez définir le niveau de journalisation et d'autres options de trace dans
le fichier de configuration de Liberty. Pour plus d'informations, voir
[Profil
Liberty : trace et journalisation](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html). Vous pouvez également ajuster le traçage sur une instance d'application en cours d'exécution à l'aide de la console IBM Bluemix.

## Utilisation des fonctions de trace et de vidage
{: #using_trace_and_dump}

Vous pouvez ajuster la configuration de traçage Liberty pour une application en cours d'exécution en procédant directement à partir de la console IBM Bluemix. La console offre aussi la possibilité de demander un vidage des unités d'exécution (threads) ou du segment de mémoire (heap). Pour ajuster la configuration de traçage ou demander un vidage, sélectionnez une application Liberty dans la console Bluemix et choisissez le menu `Exécution` dans la navigation. Dans la vue `Exécution`, sélectionnez une instance et cliquez sur le bouton *TRACE* ou *VIDAGE*. Si vous ajustez le niveau de trace, consultez [Profil Liberty : trace et journalisation](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html) pour les détails concernant la syntaxe de la spécification de trace.

### Modification de la configuration de la fonction de trace via SSH dans Diego

Dans le cas d'une application Liberty s'exécutant dans une cellule Diego, vous pouvez modifier la configuration de traçage via l'interface de ligne de commande Cloud Foundry à l'aide de la fonction SSH.

L'application envoyée par push doit inclure un fichier server.xml qui contient **updateTrigger** avec la valeur **polled**, les modifications de la spécification de traçage dans le fichier server.xml seront ensuite détectées et appliquées par l'environnement d'exécution.

Voir [Options pour l'envoi par commande push d'applications Liberty avec server.xml](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing) pour connaître les options permettant d'envoyer les applications Liberty par commande push avec un fichier server.xml personnalisé.

Voir [Contrôle des mises à jour dynamiques![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window} pour savoir comment configurer des mises à jour dynamiques dans le fichier server.xml.

Pour modifier la configuration de traçage, procédez comme suit :

1. Connectez-vous à votre application avec SSH

  ```
$ cf ssh <appname> [-i instance_index]
  ```
  {: pre}

2. Editez ```<logging traceSpecification="xxxx"/>``` dans le fichier server.xml pour définir votre spécification de trace, par exemple en utilisant *vi* :

  ```
$ vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: pre}

Remarque : Les modifications du fichier server.xml seront perdues lors d'une reconstitution ou d'un redémarrage et ne seront valides que pour l'instance à laquelle vous vous êtes connecté avec ssh.

Voir [Profil Liberty : Journalisation et trace ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window} pour obtenir des détails sur la syntaxe de la spécification de trace.

### Déclenchement de vidage via SSL dans Diego

Dans le cas d'une application s'exécutant dans une cellule Diego, vous pouvez déclencher un vidage d'unité d'exécution ou de segment de mémoire via l'interface de ligne
de commande CF en utilisant la fonction SSH. Par exemple :

  ```
$ cf ssh <appname> -c "pkill -3 java"
  ```
  {: pre}

Consultez la documentation ci-dessous pour les détails concernant le téléchargement des fichiers de vidage générés.

## Téléchargement des fichiers de vidage
{: #download_dumps}

Par défaut, les différents fichiers de vidage sont placés dans le répertoire `dumps` du conteneur de l'application.

### Application DEA

Dans le cas d'une application lancée sur un noeud DEA, utilisez la fonctionnalité "cf files" pour voir et télécharger les fichiers de vidage.

* Pour voir les vidages générés, exécutez la commande suivante :

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* Pour télécharger un fichier de vidage, exécutez les commandes suivantes :

    1. Obtenir l'identificateur global unique (GUID) de l'application

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. Télécharger le fichier de vidage

      ```
      $ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
      ```
      {: codeblock}

### Application Diego

Dans le cas d'une application lancée dans une cellule Diego, utilisez la fonctionnalité "cf ssh" pour voir et télécharger les fichiers de vidage.

* Pour voir les vidages générés, exécutez la commande suivante :

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Pour télécharger un fichier de vidage, exécutez la commande suivante :

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

Il est aussi possible d'utiliser `scp` et d'autres outils similaires pour voir et télécharger les fichiers de vidage. Pour plus d'informations, consultez [Accessing Apps with SSH![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
