---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

Les applications Liberty for Java sur {{site.data.keyword.Bluemix}} reposent sur le pack de construction liberty-for-java. Le pack de construction liberty-for-java fournit un environnement d'exécution complet permettant d'exécuter des applications Java EE 7 et OSGi par dessus WebSphere Liberty. Il prend en charge les infrastructures populaires telles que Spring et inclut l'environnement d'exécution Java {{site.data.keyword.IBM_notm}} JRE. Liberty permet un développement d'application rapide particulièrement bien adapté au cloud.
{: shortdesc}

## Détection
{: #detection}
Le pack de construction Liberty est utilisé lorsque les types d'applications suivants sont déployés :
* [Fichiers WAR](optionsForPushing.html#stand_alone_apps)
* [fichiers EAR](optionsForPushing.html#stand_alone_apps)
* [Répertoire de serveur Liberty](optionsForPushing.html#server_directory)
* [Package de serveur Liberty](optionsForPushing.html#packaged_server)
* Principal Java
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## Application de démarrage
{: #starter_application}
{{site.data.keyword.Bluemix_notm}} fournit plusieurs applications de démarrage Liberty.  Les applications de démarrage Liberty sont des applications Liberty simples qui fournissent un modèle que vous pouvez utiliser. Vous pouvez expérimenter ces applications de démarrage, puis effectuer des changements et les envoyer par commande push vers l'environnement {{site.data.keyword.Bluemix_notm}}.  Pour obtenir de l'aide sur l'utilisation des applications de démarrage, voir [Utilisation des applications de démarrage](../common/starter_app_usage.html).
