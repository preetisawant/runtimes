---

copyright:
  years: 2015, 2018
lastupdated: "2018-1-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Configuration des fonctions de journalisation et de traçage
{: #logging_tracing}

## Fichiers journaux
{: #log_files}

Les journaux Liberty standard, tels que le fichier `messages.log` ou le répertoire `ffdc`, sont disponibles dans {{site.data.keyword.Bluemix}}, dans le répertoire `logs` de chaque instance d'application. Vous pouvez accéder à ces journaux à partir de la console {{site.data.keyword.Bluemix_notm}} ou à via le client de ligne de commande pour Cloud Foundry. Par exemple :

* Pour accéder aux journaux récents d'une application, exécutez la commande suivante :

  ```
  cf logs --recent <appname>
  ```
  {: codeblock}


* Pour voir le fichier `messages.log` d'une application, exécutez la commande suivante :

  ```
  cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

Vous
pouvez définir le niveau de journalisation et d'autres options de trace dans
le fichier de configuration de Liberty. Pour plus d'informations, consultez [Traitement des incidents dans Liberty : Journalisation et Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html).

## Utilisation des fonctions de trace et de vidage
{: #using_trace_and_dump}

### Utilisation des fonctions de trace et de vidage dans la console {{site.data.keyword.Bluemix_notm}} (déprécié)

Vous pouvez ajuster la configuration de traçage Liberty pour une application en cours d'exécution en procédant directement à partir de la console {{site.data.keyword.Bluemix_notm}}. La console offre aussi la possibilité de demander un vidage des unités d'exécution (threads) ou du tas Java (heap).
Pour ajuster la configuration de traçage ou demander un vidage, sélectionnez une application Liberty dans la console {{site.data.keyword.Bluemix_notm}} et choisissez le menu `Exécution` dans la navigation. Dans la vue `Exécution`, sélectionnez une instance et cliquez sur le bouton *TRACE* ou *VIDAGE*. Si vous ajustez le niveau de trace, consultez [Traitement des incidents dans Liberty : Journalisation et Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html) pour les détails concernant la syntaxe de la spécification de trace.

### Changement de la configuration de trace via SSH

Lorsque vou poussez l'application, le fichier server.xml inclut la propriété **updateTrigger** réglée sur **polled** par défaut
et la propriété **monitorInterval** réglée à 1 minute par défaut.
Cela signifie que le serveur Liberty est automatiquement configuré pour vérifier, chaque minute, si de nouvelles mises à jour ont été apportées au fichier server.xml.

Consultez [Options pour l'envoi par commande push d'applications Liberty avec server.xml](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing) pour connaître les options permettant d'envoyer les applications Liberty par commande push avec un fichier server.xml personnalisé.

Consultez [Contrôle des mises à jour dynamiques](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window} pour savoir comment configurer des mises à jour dynamiques dans le fichier server.xml.

Suivez ces étapes pour changer la configuration de traçage :


1. Connectez-vous à votre application avec SSH

  ```
 cf ssh <appname> [-i instance_index]
  ```
  {: codeblock}

2. Editez ```<logging traceSpecification="xxxx"/>``` dans le fichier server.xml pour définir votre spécification de trace, par exemple en utilisant *vi* :

  ```
vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: codeblock}

Remarque : Les modifications du fichier server.xml seront perdues lors d'une reconstitution ou d'un redémarrage et ne seront valides que pour l'instance à laquelle vous vous êtes connecté avec ssh.

Consultez [Traitement des incidents dans Liberty : Journalisation et Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window} pour les détails concernant la syntaxe de la spécification de trace.

### Déclenchement des vidages via SSL

Pour provoquer un vidage des unités d'exécution et du tas Java via l'interface de ligne
de commande CF en utilisant la fonction SSH, utilisez la commande suivante :


  ```
 cf ssh <appname> -c "pkill -3 java"
  ```
  {: codeblock}

Consultez la documentation ci-dessous pour les détails concernant le téléchargement des fichiers de vidage générés.

## Téléchargement des fichiers de vidage
{: #download_dumps}

Par défaut, les différents fichiers de vidage sont placés dans le répertoire `dumps` du conteneur de l'application. Utilisez
l'interface de ligne de commande
de Cloud Foundry `cf ssh` pour voir et télécharger les fichiers de vidage.


* Pour voir les vidages générés, exécutez la commande suivante :

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Pour télécharger un fichier de vidage, exécutez la commande suivante :

  ```
  cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

Il est aussi possible d'utiliser `scp` et d'autres outils similaires pour voir et télécharger les fichiers de vidage. Pour plus d'informations, consultez [Accessing Apps with SSH![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
