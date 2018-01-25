---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

Les applications Liberty for Java sur {{site.data.keyword.Bluemix}} reposent sur le pack de construction liberty-for-java. Le pack de construction liberty-for-java fournit un environnement d'exécution complet permettant d'exécuter des applications Java EE 7 et OSGi par dessus le profil Liberty. Il prend en charge les infrastructures populaires telles que Spring et inclut l'environnement d'exécution Java {{site.data.keyword.IBM_notm}} JRE. WebSphere Liberty permet un développement d'application rapide particulièrement bien adapté au cloud.
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
{{site.data.keyword.Bluemix_notm}} fournit plusieurs applications de démarrage Liberty.  Les applications de démarrage Liberty sont des applications Liberty simples qui fournissent un modèle que vous pouvez utiliser. Vous pouvez expérimenter ces applications de démarrage, puis effectuer des changements et les pousser vers l'environnement {{site.data.keyword.Bluemix_notm}}. Pour obtenir de l'aide sur l'utilisation des applications de démarrage, voir [Utilisation des applications de démarrage](/docs/cfapps/starter_app_usage.html).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [Gestion des applications Liberty](/docs/manageapps/app_mng.html#Utilities)
* [Déploiement d'applications avec IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [Initiation au service IBM Monitoring and Analytics for {{site.data.keyword.Bluemix_notm}}](/docs/services/monana/index.html#monana_oview)
