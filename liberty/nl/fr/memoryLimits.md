---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Limites de mémoire et pack de construction Liberty
{: #memory_limits}

Une limite de mémoire doit être spécifiée lorsque vous déployez une application à l'aide du pack de construction Liberty.

## Limites de mémoire et pack de construction Liberty
{: #memory_limits_and_liberty}


Lorsque vous déployez une application à l'aide du pack de construction, vous êtes invité à spécifier une "Limite de mémoire". Le pack de construction Liberty for Java définit un rapport de taille de segment de mémoire par défaut pour éviter que votre processus dépasse la limite de mémoire. Vous pouvez également spécifier la taille de segment de mémoire ou le rapport en définissant les variables d'environnement `JVM_ARGS` ou `JBP_CONFIG_IBMJDK`. Voir [Options de segment de mémoire](#heap_memory_options) pour en savoir plus.

Pour déterminer la limite de mémoire à spécifier, il est important de comprendre que vous ne spécifiez pas ici la taille du segment de mémoire alloué à l'application Java. En fait, vous spécifiez la quantité de mémoire disponible pouvant être utilisée par le conteneur Diego ou l'agent DEA. Cette quantité inclut la mémoire utilisée par les composants suivants :

* par le conteneur Warden.
* pour mapper des extensions du noyau et des bibliothèques système dans le processus.
* pour les exécutables de la JVM, le segment de mémoire de travail de la JVM, l'espace JIT et les références compressées.
* pour les classes (serveur d'applications et application), les piles d'unités d'exécution et les tampons d'E-S directes.
* par le segment de mémoire alloué à l'application Java.

Pour plus d'informations sur l'utilisation de mémoire par la JVM, consultez l'article [Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/) (Merci pour cette mémoire) du site developerWorks.

Lorsque vous déployez une application, l'utilisation de mémoire par le processus complet est surveillée. Si cette utilisation dépasse la limite de mémoire que vous avez spécifiée lors du déploiement de l'application, le noyau arrête le processus. Cette action survient sans avertissement et peut se manifester de plusieurs manières.

 Si la limite de mémoire est dépassée au cours du déploiement de l'application, un message vous avertit qu'une erreur s'est produite et vous pourrez voir ce qui suit.

  * Vous pouvez peut-être constater que l'application est instable.
  * Vous pouvez éventuellement observer que l'application a tenté de démarrer à plusieurs reprises, toujours sans succès.
  * Vous pouvez recevoir un message indiquant l'échec du déploiement de l'application.

Si la limite de mémoire est dépassée alors que l'application est en service, le processus s'arrête et Cloud Foundry tente de redémarrer l'application. L'application peut redémarrer, mais reste indisponible pendant un certain temps.

## Options de segment de mémoire
{: #heap_memory_options}

Vous pouvez personnaliser de différentes manières la quantité de mémoire maximale de segment de mémoire allouée à votre application, notamment en utilisant la variable d'environnement `JVM_ARGS`, en modifiant le fichier `jvm.options` ou en définissant la variable d'environnement `JBP_CONFIG_IBMJDK` qui contrôle le paramètre `heap_size_ratio`. Si vous n'indiquez pas de paramètre, le pack de construction utilise les paramètres par défaut.

### Valeurs par défaut de segment de mémoire
{: .#heap_memory_defaults}
Pour éviter les erreurs provenant d'un dépassement des limites de mémoire, le pack de construction Liberty for Java définit un rapport de taille de segment de mémoire par défaut en fonction de la limite de mémoire que vous indiquez lors du déploiement de votre application.

* Les applications dont les limites de mémoire sont inférieures à 512M ont un rapport de taille de segment de mémoire de 50 %
* Les applications dont les limites de mémoire sont supérieures ou égales à 512M ont un rapport de taille de segment de mémoire de 75 %

Lorsque vous spécifiez le segment de mémoire à l'aide de variables d'environnement, vous remplacez les rapports de taille de segment de mémoire par défaut.

### Spécification de segment de mémoire
{: #specifying_heap_memory}

Vous pouvez définir la taille de segment de mémoire à l'aide de variables d'environnement ou en modifiant le fichier `jvm.options`. Lorsque vous utilisez les variables d'environnement `JVM_ARGS` ou `JBP_CONFIG_IBMJDK`, les modifications sont appliquées lorsque vous intégrez votre application dans {{site.data.keyword.Bluemix_notm}}. En modifiant le fichier `jvm.options`, l'effet sur la configuration de la taille de segment de mémoire peut également être testé localement.

* Utilisez la variable d'environnement `JVM_ARGS` et l'argument -Xmx. Par exemple, pour fixer à 512M la taille maximum du segment de mémoire, utilisez la commande suivante, puis reconstituez votre application.

```
    ibmcloud cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* Indiquez le rapport de taille de segment de mémoire à l'aide de la variable d'environnement JBP_CONFIG_IBMJDK.  La valeur de heap_size_ratio est une valeur en virgule flottante qui spécifie la limite de mémoire à allouer au segment de mémoire.  Par exemple, pour allouer la moitié de la mémoire disponible au segment de mémoire (50 % ou 0,50), exécutez la commande suivante et reconstituez votre application.

```
    ibmcloud cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}

* Indiquez l'argument -Xmx dans le fichier jvm.options si votre application est un [répertoire de serveur](/docs/runtimes/liberty/optionsForPushing.html#server_directory) ou un [package de serveur](/docs/runtimes/liberty/optionsForPushing.html#packaged_server). Pour plus d'informations sur l'utilisation du fichier `jvm.options` avec l'environnement d'exécution Liberty, voir [Setting generic JVM](http://www-01.ibm.com/support/docview.wss?uid=swg21596474).  
