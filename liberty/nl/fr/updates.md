---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-10"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dernières mises à jour apportées au pack de construction Liberty
{: #latest_updates}

## Liste des dernières mises à jour apportées au pack de construction Liberty.


### 10 août 2018 : Mise à jour du pack de construction v3.24-20180806-1313
* La version mensuelle de l'exécution Liberty est passée à l'édition 2018.8.0.0.
* La version de l'IBM JRE est passée au niveau 8 SR5 FP17.

### 2 juillet 2018 : Mise à jour du pack de construction Liberty v3.23-20180628-1052.
* La version par défaut de l'exécution Liberty a été mise à jour au niveau d'édition 18.0.0.2.
* La version de l'IBM JRE est passée au niveau 8 SR5 FP16.

### 8 juin 2018 : Mise à jour du pack de construction Liberty v3.22-20180601-1200.
* La version mensuelle de l'exécution Liberty est passée à l'édition 2018.6.0.0.
* La version de l'IBM JRE est passée au niveau 8 SR5 FP15.

### 11 mai 2018 : Mise à jour du pack de construction Liberty v3.21-20180509-1456.
* La version mensuelle de l'exécution Liberty est passée à l'édition 2018.5.0.0.

### 13 avril 2018 : Mise à jour du pack de construction Liberty v3.20-20180409-1221.
* La version mensuelle de l'exécution Liberty est passée à l'édition 2018.4.0.0.
* La version de l'IBM JRE est passée au niveau 8 SR5 FP11.
* L'agent de mise à l'échelle automatique a été mis à jour.

### 16 mars 2018 : Mise à jour du pack de construction Liberty v3.19-20180313-1017.
* La version par défaut de l'exécution Liberty a été mise à jour au niveau d'édition 18.0.0.1.
* La version mensuelle de l'exécution Liberty est passée à l'édition 2018.3.0.0.
* La version de l'IBM JRE est passée au niveau 8 SR5 FP10.
* La version 7 de l'IBM JRE a été retirée.  
* Le pilote DB2 JDBC est passé à la version `4.23.42`.

### 13 février 2018 : Mise à jour du pack de construction Liberty v3.18-20180213-1234.
* La version mensuelle de l'exécution Liberty est passée à l'édition 2018.2.0.0.
* La version par défaut de l'exécution Liberty inclut également le correctif temporaire [PI90804 Apache Commons interim fix]( http://www-01.ibm.com/support/docview.wss?uid=swg22011428).

### 31 janvier 2018 : Mise à jour du pack de construction Liberty v3.17.1-20180131-1532.
* Le pack de construction a été mis à jour pour inclure la fonctionnalité Liberty microProfile-1.2.

### 26 janvier 2018 : Mise à jour du pack de construction Liberty v3.17-20180122-1037.
* Le pack de construction a été mis à jour pour ajouter la possibilité de définir dynamiquement le traçage sur le serveur Liberty.
* La version mensuelle de l'exécution Liberty est passée à l'édition 2018.1.0.0.
* La version de l'IBM JRE est passée au niveau 8 SR5 FP7.

### 5 janvier 2018 : Mise à jour du pack de construction Liberty v3.16-20180102-0938.
* La version par défaut de l'exécution Liberty est passée à l'édition 17.0.0.4.
* La version mensuelle de l'exécution Liberty est passée à l'édition 2017.12.0.0.
* La version de l'IBM JRE est passée au niveau 8 SR5 FP6.


### 31 octobre 2017 : Mise à jour du pack de construction Liberty v3.15
* La version mensuelle de l'exécution Liberty est passée à l'édition 2017.10.0.0.

### 17 octobre 2017 : Mise à jour du pack de construction Liberty v3.14-20171013-1023
* La version par défaut de l'exécution Liberty est passée à l'édition 17.0.0.3.
* La version mensuelle de l'exécution Liberty est passée à l'édition 2017.9.0.1.
* La version de l'IBM JRE est passée au niveau 8 SR5.

### 5 octobre 2017 : Mise à jour du pack de construction Liberty v3.13-20170919-1721
* La version mensuelle de l'exécution Liberty est passée à l'édition 2017.9.0.0.
* La version de l'IBM JRE est passée au niveau 8 SR4 FP11.
* L'agent de mise à l'échelle automatique a été mis à jour.

### 14 août 2017 : Mise à jour du pack de construction Liberty v3.12-20170814-1322
* La version mensuelle de l'exécution Liberty a été mise à jour au niveau d'édition [2017.8.0.0](https://developer.ibm.com/wasdev/blog/2017/08/04/beta-websphere-liberty-tools-august-2017/).
* Le pack de construction contient également des environnements d'exécution Java (JRE) IBM mis à jour : version 8 SR4 FP10 et version 7.1 SR4 FP10.
* L'environnement JRE 8 comprend les fichiers Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy.
* Correction d'un bogue du pack de construction Liberty qui empêchait les applications Liberty de [s'arrêter de manière appropriée](https://docs.cloudfoundry.org/devguide/deploy-apps/app-lifecycle.html#shutdown).

### 14 juillet 2017 : Mise à jour du pack de construction Liberty v3.11-20170710-0312
* La version par défaut de l'exécution Liberty `17.0.0.2` a été mise à jour pour inclure le correctif temporaire (iFix) IFPI83713.
* La version mensuelle de l'exécution Liberty a été mise à jour au niveau d'édition [2017.7.0.0](https://developer.ibm.com/wasdev/blog/2017/07/07/beta-websphere-liberty-tools-july-2017/).
* Le pack de construction contient également des environnements d'exécution Java (JRE) IBM mis à jour : version 8 SR4 FP7 et version 7.1 SR4 FP5.
* La bibliothèque Cloudant par défaut est désormais la bibliothèque officielle [java-cloudant](https://github.com/cloudant/java-cloudant), la [bibliothèque Ektorp](https://github.com/helun/Ektorp) est toujours disponible en option. Pour obtenir des détails sur cette modification, voir l'[article du blogue](https://www.ibm.com/blogs/bluemix/2017/05/default-library-change-cloudant-auto-wiring-liberty-buildpack/).
* Le rapport de taille de segment de mémoire est désormais 50 % lorsque votre application dispose de moins de 512mb de mémoire, si elle dispose de plus de 512mb, il aura la valeur 75 %.
* Un nouveau journal des tâches de préproduction est désormais généré, ce qui permet de faciliter le débogage des erreurs en préproduction.
* L'environnement d'exécution Node.js utilisé par l'[utilitaire App Management](../common/app_mng.html) a été mis à jour à la version 6.13.0.
* Le pack de construction fournit également un agent mis à jour pour le [service de mise à l'échelle automatique](/docs/services/Auto-Scaling/index.html).

### 12 juin 2017 : Mise à jour du pack de construction Liberty v3.10-20170525-1107
* La version par défaut de l'exécution Liberty a été mise à jour au niveau d'édition 17.0.0.2.
* La version mensuelle de l'exécution Liberty a été mise à jour au niveau d'édition [2017.5.0.0](https://developer.ibm.com/wasdev/blog/2017/05/12/beta-websphere-liberty-tools-may-2017/).
* L'environnement d'exécution Node.js utilisé par l'[utilitaire App Management](../common/app_mng.html) a été mis à jour à la version 6.10.0.
* Le pack de construction fournit également une version mise à jour d'Extreme Scale Client.

### 27 avril 2017 : Mise à jour du pack de construction Liberty v3.9-20170419-1403
* La version par défaut de l'exécution Liberty `17.0.0.1` a été mise à jour pour inclure les correctifs temporaires [PI77770](http://www-01.ibm.com/support/docview.wss?uid=swg24043596), [PI77605](http://www-01.ibm.com/support/docview.wss?uid=swg1PI77605), [PI79275](http://www-01.ibm.com/support/docview.wss?uid=swg1PI79275) et PI77438.
* La version mensuelle de l'exécution Liberty a été mise à jour au niveau d'édition [2017.3.0.0](https://developer.ibm.com/wasdev/blog/2017/03/14/beta-websphere-liberty-tools-march-2017/).
* Le calcul de la mémoire est passé de la préproduction au processus de démarrage, facilitant ainsi les changements de segment de mémoire avec le redémarrage d'une application.
* Le pack de construction fournit également des versions mises à jour de l'agent pour le [service de mise à l'échelle automatique](/docs/services/Auto-Scaling/index.html) et Extreme Scale Client.

### 14 mars 2017 : Mise à jour du pack de construction Liberty v3.8-20170308-1507
* La version par défaut de l'exécution Liberty est passée à l'édition 17.0.0.1.
* La version par défaut de l'exécution Liberty inclut également le correctif temporaire (iFix) PI75512 pour la fonctionnalité WebSockets.
* La version mensuelle de l'exécution Liberty est passée à l'édition [2017.2.0.0](https://developer.ibm.com/wasdev/blog/2017/02/17/beta-websphere-liberty-tools-february-2017/).
* Les versions 8 et 7.1 de l'IBM JRE sont passées au niveau SR4 FP1.
* Le support de configuration automatique a été étendu pour fonctionner avec [ibm-websphere-extreme-scale (IBM Container)](https://console.ng.bluemix.net/docs/images/docker_image_extreme_scale/ibm-websphere-extreme-scale_starter.html).
* Le support de configuration automatique pour [Cloudant NoSQL Database](https://console.ng.bluemix.net/docs/services/Cloudant/index.html) a été mis à jour pour permettre l'utilisation de la bibliothèque Cloudant pour Java à la place de org.ektorp. Pour activer l'utilisation de cette bibliothèque, vous devez configurer la variable d'environnement suivante :    
```
ibmcloud cf set-env <appName> LBP_SERVICE_CONFIG_CLOUDANTNOSQLDB 'type : cloudant'
```
* Le pack de construction fournit aussi une version mise à jour de l'agent pour le [service de mise à l'échelle automatique](/docs/services/Auto-Scaling/index.html) ainsi qu'un certain nombre d'évolutions dans la gestion des applications.
* Le pack de construction apporte également des changements dans le fonctionnement de la configuration automatique pour le service Monitoring and Analytics. La capacité de journalisation ne sera plus ajoutée aux applications qui utilisent le plan gratuit, cette capacité étant actuellement remplacée par logmet.  


### 23 janvier 2017 : Mise à jour du pack de construction Liberty v3.7-20170118-2046
* La version mensuelle de l'exécution Liberty est passée à l'édition [2017.1.0.0](https://developer.ibm.com/wasdev/blog/2017/01/20/beta-websphere-liberty-tools-january-2017/).
* L'IBM JRE version 8 est passé au niveau SR3 FP22.
* Le support de [configuration automatique](autoConfig.html) a également été étendu pour fonctionner avec le [service Compose for MongoDB](https://console.ng.bluemix.net/docs/services/ComposeForMongoDB/index.html) (actuellement seulement disponible avec l'exécution Liberty mensuelle).

### 13 décembre 2016 : Mise à jour du pack de construction Liberty v3.6-20161209-1351
* La version par défaut de l'exécution Liberty est passée à l'édition[16.0.0.4](http://www-01.ibm.com/support/docview.wss?uid=swg27009661).
* L'IBM JRE version 8 est passé au niveau SR3 FP21.
* Le support de [configuration automatique](autoConfig.html) a également été étendu pour fonctionner avec le [service Compose for PostgreSQL](https://console.ng.bluemix.net/docs/services/ComposeForPostgreSQL/index.html).
* Le pack de construction fournit aussi une version mise à jour de l'agent pour le [service de mise à l'échelle automatique](/docs/services/Auto-Scaling/index.html).
* Le pack de construction a été mis à jour pour fonctionner avec les fichiers de variables d'environnement inclus dans le fichier `server.xml` (via une entrée spécifique 'include location').

### 29 novembre 2016 : Mise à jour du pack de construction Liberty v3.5-20161114-1152
* L'exécution Liberty par défaut version `16.0.0.3` a été mise à jour pour inclure le correctif temporaire (iFix) [PI62375](https://www-01.ibm.com/support/docview.wss?uid=swg24042712) et fournir la fonction de commodité `microProfile-1.0`.
* La version mensuelle de l'exécution Liberty est passée à l'édition `2016.11.0.0`.
* Le pack de construction contient également une mise à jour des deux versions de l'IBM JRE : SR3 FP20 pour la version 8 et SR3 FP60 pour la version 7.1.
* Le pilote DB2 JDBC est passé à la version `4.21.29`.
* L'intégration du service Monitoring and Analytics a été corrigée pour fonctionner avec [Diego ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.cloudfoundry.org/concepts/diego/diego-architecture.html).
* Les intégrations de service [Dynatrace](dynatrace.html) ont été mises à jour de manière à améliorer leur fonctionnement avec les offres de service Dynatrace.
* Le support de [configuration automatique](autoConfig.html) pour les types de services PostgreSQL et MySQL a été amélioré de manière à mieux fonctionner lors du déploiement d'un répertoire de serveur ou d'un serveur en package.
* L'exécution Node.js avec laquelle fonctionnent les [utilitaires devconsole et shell d'App Management](../common/app_mng.html#app_management) est passée à la dernière version, `0.12.17`.
* Les [correctifs de sécurité](http://www.ibm.com/support/docview.wss?uid=swg21994945) de l'environnement d'exécution Liberty sont inclus.

### 1 novembre 2016 : Mise à jour du pack de construction Liberty v3.4.1-20161030-2241
* Le pack de construction contient un correctif destiné à remédier à un problème lié au démarrage de certains types d'application. En particulier, les applications déployées en tant que répertoire de serveur ou package de serveur avec les fichiers d'application dans le répertoire `dropins`.

### 21 octobre 2016 : Mise à jour du pack de construction Liberty v3.4-20161018-2004
* La version d'exécution Liberty par défaut `16.0.0.3` a été mise à jour pour inclure les correctifs temporaires [PI68805](http://www-01.ibm.com/support/docview.wss?uid=swg1PI68805) et [PI69141](http://www-01.ibm.com/support/docview.wss?uid=swg1PI69141).
* La version d'exécution Liberty mensuelle a été mise au niveau de l'édition [2016.9.0.1](https://developer.ibm.com/wasdev/blog/2016/09/23/beta-websphere-liberty-and-tools-october-2016/).
* Le pack de construction contient également une version mise à jour de l'environnement IBM JRE 8.0 : SR3 FP12.
* Les environnements IBM JRE 8.0 et 7.1 sont désormais configurés pour activer [tous les protocoles TLS lorsque `SSLContext.getContext("TLS")` est appelé](https://www.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.security.component.80.doc/security-component/jsse2Docs/matchsslcontext_tls.html) afin de correspondre au comportement du JRE d'Oracle. L'environnement IBM JRE 7.1 est également configuré pour activer [tous les protocoles TLS lorsque `SSLContext.getDefault()` est appelé](https://www.ibm.com/support/knowledgecenter/SSYKE2_7.1.0/com.ibm.java.security.component.71.doc/security-component/jsse2Docs/overrideSSLprotocol.html) pour correspondre au comportement du JRE 8.0 d'IBM.
* Le pack de construction fournit un collecteur de données mis à jour pour le service Monitoring and Analytics.
* Le pack de construction a été restauré pour télécharger le [pilote JDBC MariaDB Connector/J ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/) le plus récent lors de la [configuration automatique du type de service MySQL](autoConfig.html).
* Le pack de construction comprend la prise en charge de la personnalisation du comportement de configuration automatique des services via la variable d'environnement `LBP_SERVICE_CONFIG_<serviceType>`. Il peut ainsi être employé pour modifier l'emplacement ou la version d'un pilote JDBC à télécharger pour le service MySQL. Pour plus d'informations, voir la documentation relative aux [services qui prennent en charge la configuration automatique](autoConfig.html).
* Le pack de construction contient également un certain nombre d'améliorations [Diego![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.cloudfoundry.org/concepts/diego/diego-architecture.html) liées au diagnostic d'intégrité d'application et à la fonctionnalité [App Management](../common/app_mng.html).

### 16 septembre 2016 : Mise à jour du pack de construction Liberty v3.3-20160912-1729
* La version d'exécution Liberty par défaut a été mise au niveau de l'édition [16.0.0.3](http://www-01.ibm.com/support/docview.wss?uid=swg27009661). La version d'exécution Liberty mensuelle a été mise au niveau de l'édition [2016.9.0.0](https://developer.ibm.com/wasdev/blog/2016/08/26/beta-websphere-liberty-and-tools-september-2016/). Avec ces mises à jour, les fonctions Liberty `cloudant-1.0` et `passwordUtilities-1.0`, disponibles auparavant en tant que fonctions bêta, sont désormais disponibles en tant que fonctions prêtes pour la production.
* Les [correctifs de sécurité](http://www-01.ibm.com/support/docview.wss?uid=swg21990527) de l'environnement d'exécution Liberty sont inclus.
* Le pack de construction contient également une version mise à jour de l'environnement IBM JRE 8.0 : SR3 FP11.
* Le pack de construction a été ajusté pour télécharger le dernier niveau du [pilote JDBC MariaDB Connector/J![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/) lors de l'exécution de la [configuration automatique du type MySQL de services](autoConfig.html), du fait d'un problème avec le dernier pilote 1.5.x.

### 26 août 2016 : Mise à jour du pack de construction Liberty v3.2-20160822-2200
* Le pack de construction contient également les versions mises à jour d'IBM JRE : 8 SR3 FP10 et 7.1 SR3 FP50.
* La version d'exécution Liberty mensuelle a été mise au niveau de l'édition [2016.8.0.0](https://developer.ibm.com/wasdev/blog/2016/07/28/beta-websphere-liberty-and-tools-august-2016/).
* Le plug-in de service qui fournit le [support de configuration automatique](autoConfig.html) pour le service [SQL Database](/docs/services/SQLDB/index.html#SQLDB) a été mis à jour pour toujours utiliser les certificats sécurisés JVM lors de la connexion au service sur TLS.

### 22 juillet 2016 : Mise à jour du pack de construction Liberty v3.1-20160717-2254
* La fonctionnalité [Gestion de l'appli](../common/app_mng.html) a été mise à jour pour prendre en charge l'authentification fédérée. De plus, le contexte d'exécution Node.js dont se servent les utilitaires `devconsole` et `shell` a été mis à jour vers la version la plus récente, `0.12.15`.
* Le pack de construction ajoute une prise en charge de l'agent de surveillance d'application [Dynatrace Ruxit![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.dynatrace.com/en/ruxit/).
* Le pack de construction fournit un collecteur de données mis à jour pour le service Monitoring and Analytics.
* Le pack de construction fournit aussi une version mise à jour de l'agent pour le [service de mise à l'échelle automatique](/docs/services/Auto-Scaling/index.html).
* La version d'exécution Liberty mensuelle a été mise au niveau de l'édition [2016.7.0.0](https://developer.ibm.com/wasdev/blog/2016/06/30/beta-websphere-liberty-and-tools-july-2016/).

### 17 juin 2016 : Mise à jour du pack de construction Liberty v3.0-20160608-1450
* Le pack de construction contient désormais deux versions de WebSphere Liberty (la dernière édition stable et la dernière édition mensuelle). Plus spécifiquement, il fournit l'édition stable [16.0.0.2](http://www-01.ibm.com/support/docview.wss?uid=swg21984970) et l'édition mensuelle [2016.6.0.0](https://developer.ibm.com/wasdev/blog/2016/06/03/beta-websphere-liberty-and-tools-june-2016/). L'édition stable sera utilisée par défaut. Pour plus d'informations, voir [Liberty versions](buildpackDefaults.html#liberty_versions).
* Le pack de construction contient aussi les correctifs de sécurité suivants : [Security Bulletin: Vulnerability in Apache Standard Taglibs affects Liberty for Java for IBM Bluemix (CVE-2015-0254)](http://www-01.ibm.com/support/docview.wss?uid=swg21985531).

### 25 mai 2016 : Mise à jour du pack de construction Liberty v2.9-20160519-1249
* Le pack de construction contient une version mise à jour de WebSphere Liberty basée qui repose sur la [version bêta de mai](https://developer.ibm.com/wasdev/blog/2016/05/06/beta-websphere-liberty-and-tools-may-2016/). La version mise à jour de Liberty met à disposition les fonctions bêta *bluemixLogCollector-1.1* et *logstashCollector-1.1* dans {{site.data.keyword.Bluemix_notm}}.

### 5 mai 2016 : Mise à jour du pack de construction Liberty v2.8-20160430-1011
* Le pack de construction contient une version mise à jour de WebSphere Liberty qui repose sur la [version bêta d'avril](https://developer.ibm.com/wasdev/blog/2016/04/08/beta-websphere-liberty-and-tools-april-2016/). La version mise à jour de Liberty met à disposition la fonction GA *logstashCollector-1.0* et la fonction bêta *logmetCollector-1.0* dans {{site.data.keyword.Bluemix_notm}}.
* Le pack de construction contient également les versions mises à jour d'IBM JRE : 8 SR3 et 7.1 SR3 FP40.
* Le pack de construction ajoute la prise en charge initiale de l'agent de surveillance d'application [AppDynamics![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.appdynamics.com/).
* La prise en charge de [Dynatrace](dynatrace.html) a été améliorée afin de simplifier l'installation de l'agent.
* Le pack de construction fournit un collecteur de données mis à jour pour le service Monitoring and Analytics. Il contient un correctif destiné à remédier un problème lié à la collecte de données de segment de mémoire maximales.
* L'exécution Node.js avec laquelle fonctionnent les [utilitaires devconsole et shell d'App Management](../common/app_mng.html#app_management) est passée à la dernière version, 0.12.13.

### 25 mars 2016 : Mise à jour du pack de construction Liberty v2.7-20160321-1358
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la [version bêta de mars](https://developer.ibm.com/wasdev/blog/2016/03/18/new-websphere-liberty-features-march-2016/). La version mise à jour de Liberty met à disposition la fonction bêta cloudant-1.0 dans {{site.data.keyword.Bluemix_notm}}.
* Le pack de construction contient également les versions mises à jour suivantes d'IBM JRE : 8 SR2 FP12 et 7.1 SR3 FP32.
* Le pack de construction fournit une version mise à jour de l'agent pour le [service Auto-Scaling](/docs/services/Auto-Scaling/index.html).
* Le pack de construction comporte désormais un nouveau collecteur de données pour le service Monitoring and Analytics. Le nouveau collecteur active la configuration des seuils de surveillance et contient un certain nombre de correctifs de bogue.
* Le pack de construction fournit un pilote JDBC DB2 version 4.19.49 mis à jour.
* L'exécution Node.js avec laquelle fonctionnent les [utilitaires devconsole et shell d'App Management](../common/app_mng.html#app_management) est passée à la dernière version, 0.12.12.

### 7 mars 2016 : Mise à jour du pack de construction Liberty v2.6-20160225-1649
* Le pack de construction ajoute la prise en charge de la surveillance d'applications Dynatrace. Pour plus d'informations, voir [Utilisation de Dynatrace](dynatrace.html).
* Le pack de construction ajoute la prise en charge de [DynamicPULSE](www.fujitsu.com/jp/group/fsweb/products/dynamic-pulse/).

### 10 février 2016 : Mise à jour du pack de construction Liberty v2.5-20160209-1336
* Le pack de construction contient une version mise à jour de WebSphere Liberty qui repose sur la [version bêta de février](https://developer.ibm.com/wasdev/blog/2016/02/12/beta-websphere-liberty-and-tools-february/). La version mise à jour du profil Liberty met à disposition la fonction GA apiDiscovery-1.0 dans {{site.data.keyword.Bluemix_notm}}.

### 4 février 2016 : Mise à jour du pack de construction Liberty v2.4-20160127-1437
* Le pack de construction contient une version mise à jour de WebSphere Liberty qui repose sur la version bêta de janvier. Avec cette mise à jour, la fonction Liberty sp-2.3, auparavant disponible en tant que fonction bêta, est désormais disponible en tant que fonction prêtes pour la production. La version mise à jour de Liberty met également à disposition la fonction bêta passwordUtilities-1.0 dans {{site.data.keyword.Bluemix_notm}}.
* Le pack de construction contient également les environnements d'exécution Java IBM JRE 7.1 SF3 FP20 et IBM JRE 8 SR2 FP10 mis à jour.
* Le pack de construction a été mis à jour pour télécharger le dernier niveau du [pilote JDBC MariaDB Connector/J![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/) 1.x lors de l'exécution de la [configuration automatique du type de service MySQL](autoConfig.html).

### 16 décembre 2015 : Mise à jour du pack de construction Liberty v2.3-20151208-1311
* Le pack de construction contient également une version mise à jour du profil Liberty basée sur la [version bêta de décembre](https://developer.ibm.com/wasdev/blog/2015/11/20/beta-was-liberty-beta-with-tools-december-2015/). La version mise à jour du profil Liberty met à disposition dans {{site.data.keyword.Bluemix_notm}} les fonctions GA pnego-1.0 et wsSecuritySaml-1.1, ainsi que la fonction bêta scim-1.0.
* Le pack de construction contient également un environnement d'exécution Java IBM JRE 8 SR2 mis à jour.
* Le pack de construction a été mis à jour pour télécharger le dernier niveau du [pilote JDBC PostgreSQL 9.4.x ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://jdbc.postgresql.org/) et du [pilote JDBC MariaDB Connector/J![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/) 1.2.x lors de l'exécution de la [configuration automatique](autoConfig.html) des types de service PostgreSQL ou MySQL.

### 23 novembre 2015 : Mise à jour du pack de construction Liberty v2.2-20151119-1720
* Le pack de construction contient une version mise à jour de l'environnement d'exécution du profil Liberty et du client WebSphere eXtreme Scale avec des correctifs de sécurité pour [la vulnérabilité d'Apache Commons Collection](http://www-01.ibm.com/support/docview.wss?uid=swg21971426).
* Le pack de construction contient également une version mise à jour du [pilote Java MongoDB ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.mongodb.org/ecosystem/drivers/java/) version 2.13.3. Le nouveau pilote est compatible avec MongoDB versions 2.4, 2.6 et 3.0.
* Le pack de construction fournit également une version mise à jour du collecteur de données pour le service Monitoring and Analytics. Le collecteur de données mis à jour propose des fonctions de trace de méthode améliorées.

### 16 octobre 2015 : Mise à jour du pack de construction Liberty v2.1-20151006-0912
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la [version bêta d'octobre](https://developer.ibm.com/wasdev/blog/2015/09/25/beta-was-liberty-beta-with-tools-october-2015/). Avec cette mise à jour, les fonctions Liberty bells-1.0, rtcomm-1.0, rtcommGateway-1.0, samlWeb-2.0 et sipServlet-1.1, auparavant disponibles en tant que fonctions bêta, sont désormais disponibles en tant que fonctions prêtes pour la production.
* Le pack de construction contient également un environnement d'exécution Java IBM JRE 8 SR1 FP11 mis à jour.
* Le pack de construction contient également plusieurs optimisations et améliorations des performances :
  * La fonction d'examen des archives de bean implicites [CDI 1.2](optionsForPushing.html) est désactivée par défaut lors du déploiement des fichiers WAR ou EAR.
  * Pour réduire la taille des gouttelettes, les [utilitaires App Management](../common/app_mng.html) devconsole et shell requièrent une opération de reconstitution au lieu d'un redémarrage.
  * Le cache de classes partagées du JRE IBM est désactivé car il n'était pas réutilisé dans l'environnement {{site.data.keyword.Bluemix_notm}}.

### 18 septembre 2015 : Mise à jour du pack de construction Liberty v2.0-20150914-1535
* Le pack de construction présente deux changements majeurs :
  * La configuration par défaut pour les fichiers WAR et EAR active des fonctions du profil Web Java EE 7 au lieu de fonctions du profil Web Java EE 6.
  * La version Java par défaut est la version 8 au lieu de la version 7.
* Pour plus d'informations sur ces changements et leur impact sur votre application, voir l'article blogue [Upcoming Liberty for Java buildpack changes](https://developer.ibm.com/bluemix/2015/09/08/upcoming-liberty-for-java-buildpack-changes/).
* Le pack de construction contient également une nouvelle option de configuration, app_state, qui permet de désactiver la fonction appstate via la variable d'environnement JBP_CONFIG_LIBERTY. La fonction appstate est intégrée au processus de diagnostic d'intégrité Cloud pour vérifier que l'application Liberty est entièrement initialisée de sorte que l'application puisse recevoir des demandes HTTP. Pour désactiver la fonction appstate, vous pouvez associer la variable d'environnement JBP_CONFIG_LIBERTY à la valeur "app_state: false".

### 4 septembre 2015 : Mise à jour du pack de construction Liberty v1.22-20150824-1104
* Le pack de construction prend en charge les [variables d'environnement HTTP_PROXY et HTTPS_PROXY](environmentVariables.html). Si elles sont définies, le pack de construction utilise le serveur proxy qu'elles spécifient lorsqu'il télécharge divers composants de pack de construction.

### 19 août 2015 : Mise à jour du pack de construction Liberty v1.21-20150811-1342
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la [version bêta d'août](https://developer.ibm.com/wasdev/blog/2015/07/30/beta-was-liberty-beta-with-tools-august-2015/). La version mise à jour du profil Liberty met à disposition les nouvelles [fonctions bêta](usingBetaFeatures.html) suivantes dans {{site.data.keyword.Bluemix_notm}} : bells-1.0, rtcommGateway-1.0, samlWebSso-2.0.

### 31 juillet 2015 : Mise à jour du pack de construction Liberty v1.20.1-20150729-1255
* Le pack de construction contient des versions mises à jour des environnements d'exécution Java (JRE) d'IBM : 7.1 SR1 FP10 et 8 SR1 FP10.
Les environnements d'exécution Java (JRE) mis à jour contiennent les [correctifs de sécurité les plus récents](http://www-01.ibm.com/support/docview.wss?uid=swg21964161) ainsi que d'autres améliorations.
* Le plug-in de service qui fournit le [support de configuration automatique](autoConfig.html) pour le service [Cloudant NoSQL Database](/docs/services/Cloudant/index.html#Cloudant) a été mis à jour pour garantir que les connexions au service sont établies sur un canal sécurisé.

### 21 juillet 2015 : Mise à jour du pack de construction Liberty v1.20-20150713-1450
* Le pack de construction contient une version mise à jour du profil Liberty en fonction de l'[édition 8.5.5.6](https://developer.ibm.com/wasdev/blog/2015/06/25/java-ee-7-has-landed-in-was-liberty/). Avec cette édition, toutes les fonctions Liberty Java EE 7 disponibles auparavant en tant que fonctions bêta sont désormais disponibles en tant que fonctions prêtes pour la production. En raison des restrictions de port et autres restrictions dans {{site.data.keyword.Bluemix_notm}}, certaines fonctions telles que les EJB distants ne sont pas intégralement prises en charge sur la plateforme.
* Le pack de construction reconnaît et exécute des packages d'applications avec [distZip-style![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.gradle.org/current/userguide/application_plugin.html).
* Le pack de construction contient un collecteur de données mis à jour pour le service Monitoring and Analytics ainsi que le client WebSphere eXtreme Scale qui prennent en charge la nouvelle version de l'exécution Liberty.

### 30 juin 2015 : Mise à jour du pack de construction Liberty v1.19.1-20150622-1509
* Cette version du pack de construction contient un environnement d'exécution Java IBM JRE mis à jour avec un correctif de sécurité pour la [vulnérabilité LogJam](http://www-01.ibm.com/support/docview.wss?uid=swg21961390).
* L'agent [New Relic](newRelic.html) a été mis à jour vers la version 3.17. La nouvelle version propose une intégration améliorée à l'environnement d'exécution du profil Liberty.

### 14 juin 2015 : Mise à jour du pack de construction Liberty v1.19-20150608-1717
* Le pack de construction contient plusieurs améliorations de la gestion des applications, notamment la prise en charge de la console de développement et un accès Web à l'interpréteur de commandes. Pour plus d'informations, voir la [documentation relative à la gestion des applications](../common/app_mng.html).
* Le pack de construction contient également un correctif visant à résoudre un problème qui empêchait de trouver la fonction Liberty pour le service Monitoring and Analytics.

### 27 mai 2015 : Mise à jour du pack de construction Liberty v1.18-20150519-1642
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la [version bêta de mai](https://developer.ibm.com/wasdev/blog/2015/05/08/beta-liberty-and-tools-may-2015/).

### 5 mai 2015 : Mise à jour du pack de construction Liberty v1.17-20150501-1729
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la [version bêta d'avril](https://developer.ibm.com/wasdev/blog/2015/04/10/announcing-liberty-beta-with-tools-aprilmay-2015/). Avec cette mise à jour, les fonctions Liberty sp-2.3, el-3.0 et jdbc-4.1 L, disponibles auparavant en tant que fonctions bêta, sont désormais disponibles en tant que fonctions prêtes pour la production. De plus, des fonctions Java EE 7 supplémentaires telles que jsf-2.2, javaMail-1.5, webProfile-7.0 et javaee-7.0, sont désormais disponibles en tant que [fonctions bêta](usingBetaFeatures.html).
* Le pack de construction fournit également le support initial pour Java 8. IBM JRE 7.1 reste l'environnement d'exécution Java par défaut mais vous pouvez activer IBM JRE 8 pour une application en définissant la variable d'environnement JBP_CONFIG_IBMJDK. La configuration de la version d'OpenJDK est également prise en charge. Voir [Personnalisation de l'environnement d'exécution Java (JRE)](customizingJRE.html) pour des détails.
* Le pack de construction fournit une nouvelle variable d'environnement JBP_CONFIG_LIBERTY que vous pouvez utiliser pour remplacer le jeu par défaut de fonctions Liberty activées pour une application lors du déploiement d'un fichier WAR ou EAR. Voir [Applications autonomes](optionsForPushing.html#stand_alone_apps) pour plus d'informations.
* Le plug-in du service Monitoring and Analytics a été mis à jour afin de réduire la taille des journaux générés pour le service.
* Avec cette version du pack de construction, la façon dont les fichiers d'application sont présentés dans la gouttelette a changé. La modification apportée à la structure de fichier élimine la complexité relative à la gestion des liens symboliques et ne devrait pas avoir d'impact sur les applications.

### 15 avril 2015 : Mise à jour du pack de construction Liberty v1.16-20150407-1737
* Cette version du pack de construction contient un environnement d'exécution Java IBM JRE 7.1-2.11 mis à jour avec un [correctif de sécurité pour la vulnérabilité Bar Mitzvah](http://www-01.ibm.com/support/docview.wss?uid=swg21882777).
* Lorsque des fichiers WAR autonomes sont déployés, si mis à disposition, le pack de construction utilise désormais la racine de contexte qui est spécifiée dans le fichier **ibm-web-ext.xml** imbriqué comme racine de contexte de l'application. Suite à cette modification, les applications qui étaient auparavant déployées sous le contexte racine peuvent être déployées sous un contexte différent en fonction des paramètres figurant dans le fichier **ibm-web-ext.xml**.

### 3 avril 2015 : Mise à jour du pack de construction Liberty v1.15-20150402-1422
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la [version bêta de mars](https://developer.ibm.com/wasdev/blog/2015/03/13/announcing-liberty-beta-tools-march-2015/). La version mise à jour des profils Liberty met à disposition la fonction bêta jsf-2.2 dans {{site.data.keyword.Bluemix_notm}}.
* Le pack de construction contient également une version mise à jour du collecteur de données pour le service Monitoring and Analytics.

### 20 mars 2015 : Mise à jour du pack de construction Liberty v1.14-20150319-1159
* Cette version du pack de construction contient un environnement d'exécution Java IBM JRE 7.1.2.11 mis à jour avec un correctif de sécurité pour la [vulnérabilité FREAK](http://www-01.ibm.com/support/docview.wss?uid=swg21699864).
* Le service [ SQL Database](services/SQLDB/index.html#SQLDB) propose des plans payants qui permettent de se connecter au serveur de base de données via le protocole SSL. La prise en charge de la configuration automatique du pack de construction pour le service SQL Database a été mise à jour pour configurer l'environnement d'exécution en vue de la connexion à la base de données via SSL si les informations de connexion SSL sont disponibles.
* Le pack de construction a été mis à jour pour signaler une erreur lorsqu'un fichier WAR ou EAR autonome contenant un fichier de configuration **server.xml** dans la racine de l'archive d'application est déployé.
* Le pack de construction contient un correctif pour le plug-in de service de configuration automatique de MongoDB qui, dans certains cas, générait une configuration **server.xml** non valide.

### 10 février 2015 : Mise à jour du pack de construction Liberty v1.13-20150209-1122
* Le pack de construction contient des correctifs de sécurité pour les [vulnérabilités d'Apache HttpComponents et de la fonction de surimposition Java](https://www-304.ibm.com/connections/blogs/PSIRT/entry/ibm_security_bulletin_multiple_vulnerabilities_fixed_in_liberty_for_java_for_ibm_bluemix_cve_2012_6153_cve_2014_3577_cve_2015_0178?lang=en_us).
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la [version bêta de février](https://developer.ibm.com/wasdev/blog/2015/02/13/announcing-liberty-beta-tools-february-2015/). La version mise à jour du profil Liberty fournit une version mise à jour de la fonction WebSocket GA websocket-1.1. Elle met également à disposition les fonctions bêta Java EE 7 suivantes dans {{site.data.keyword.Bluemix_notm}} :
  * cdi-1.2, el-3.0, jsp-2.3, jca-1.7, jacc-1.5 et jaspic-1.1
* Le pack de construction fournit l'intégration à l'[outil JRebel de ZeroTrunaround![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://zeroturnaround.com/software/jrebel/). L'intégration facilite l'utilisation de JRebel avec les applications {{site.data.keyword.Bluemix_notm}} et permet de les mettre à jour instantanément sans qu'il soit nécessaire de les redéployer ou de les reconstituer. Les applications Web autonomes seulement sont prises en charge.

### 6 février 2015 : Mise à jour du pack de construction Liberty v1.12-20150130-1016
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la [version bêta de janvier](https://developer.ibm.com/wasdev/blog/2015/01/16/announcing-liberty-beta-tools-january-2015/).
* Le pack de construction contient une version épurée du collecteur de données pour le service Monitoring and Analytics.

### 23 janvier 2015 : Mise à jour du pack de construction Liberty v1.11-20150119-1511
* Le pack de construction contient un environnement d'exécution Java IBM JRE version 7.1 SR2 FP1 mis à jour.
* Il contient également un client WebSphere eXtreme Scale version 8.6.0.6 mis à jour et un agent mis à jour pour le service Auto-Scaling.
* La prise en charge du service [New Relic](newRelic.html) a été améliorée pour prendre en charge les services définis par l'utilisateur.
* Le pack de construction a été amélioré pour indiquer les versions détaillées du profil Liberty et d'IBM JRE.

### 19 décembre 2014 : Mise à jour du pack de construction Liberty v1.10-20141218-0103
* Le pack de construction fournit un mode développement pour les applications. Il s'agit d'un mode spécial qui permet aux développeurs d'effectuer de nombreuses opérations avec une instance d'application, opérations qui n'étaient pas possibles auparavant. Grâce à cette fonction, cette version de {{site.data.keyword.eclipsetoolsfull}} peut désormais prendre en charge le débogage à distance avec des mises à jour de fichier incrémentielles pour une application Liberty qui s'exécute dans {{site.data.keyword.Bluemix_notm}}. Ainsi, un développeur peut utiliser facilement Eclipse pour déboguer une application dans le cloud et lui apporter des changements instantanément.
* Le pack de construction contient également une version mise à jour du profil Liberty basée sur la version [bêta de décembre](https://developer.ibm.com/wasdev/blog/2014/12/10/announcing-liberty-beta-december/).
* En outre, les quatre fonctions Liberty suivantes qui étaient auparavant disponibles en tant que fonctions bêta, sont désormais prêtes pour la production :
  * concurrent-1.0
  * jsonp-1.0
  * servlet-3.1
  * websocket-1.0.
* Le pack de construction fournit l'intégration au service New Relic. Une fois qu'une application est liée au service New Relic, le pack de construction télécharge et configure automatiquement l'environnement d'exécution avec l'agent New Relic.
* Les limitations connues suivantes existent pour le pack de construction :
  * En mode développement, un service SessionCache ne peut pas être lié.
  * En mode développement, il n'est pas possible de créer un cliché de l'unité d'exécution.
  * Lorsque vous utilisez la fonction servlet-3.1 ou websocket-v1.0, le service Monitoring & Analytics est introuvable.

### 5 décembre 2014 : Mise à jour du pack de construction Liberty v1.9-20141202-0947
* Le pack de construction fournit une prise en charge améliorée des options JVM. Les options JVM peuvent désormais être appliquées avec une opération de redémarrage. Il n'est pas nécessaire de constituer l'application. Les options JVM par défaut sont optimisées pour le mode "Fast failure" et préconfigurées avec un emplacement général qui facilite la localisation des clichés générés. Pour plus d'informations, voir l'article [Custom Configuration of Java JVM for the Liberty Runtime](https://developer.ibm.com/bluemix/2014/12/12/custom-configurations-java-jvm-liberty-runtime/).
* Le pack de construction contient un pilote JDBC DB2 version 4.17.29 mis à jour.
* Il contient également le correctif d'un problème qui empêchait la collecte des informations relatives à l'utilisation du pool d'unités d'exécution Liberty pour le service Monitoring & Analytics.

### 21 novembre 2014 : Mise à jour du pack de construction Liberty v1.8-20141118-1610
* Le pack de construction contient un environnement d'exécution Java IBM JRE version 7.1 SR2 mis à jour qui fournit un correctif pour la [vulnérabilité POODLE](http://www-01.ibm.com/support/docview.wss?uid=swg21687173).
* Il contient également une version mise à jour du profil Liberty basée sur le profil [bêta de novembre](https://developer.ibm.com/wasdev/blog/2014/11/07/announcing-liberty-profile-beta-november/).

### 30 octobre 2014 : Mise à jour du pack de construction Liberty v1.7-20141020-1759
* Le pack de construction contient un environnement d'exécution Java IBM JRE version 7.1 SR1 FP3 mis à jour.
* Il fournit également le correctif d'un problème qui empêchait le déploiement des applications avec une configuration de serveur contenant des caractères Unicode.

### 23 octobre 2014 : Mise à jour du pack de construction Liberty v1.6-20141013-1628
* e pack de construction comporte désormais un nouveau collecteur de données pour le service Monitoring and Analytics. Le nouveau collecteur de données collecte des informations de diagnostic approfondies qui permettent aux utilisateurs du plan Diagnostics du service de diagnostiquer les problèmes affectant leurs applications, en traçant leur origine jusqu'à la ligne de code spécifique concernée.
* Le pack de construction contient des versions mises à jour des agents de gestion et de mise à l'échelle qui comprennent des correctifs de bogue et des améliorations mineures. Il inclut également une version mise à jour du [profil Liberty](https://developer.ibm.com/wasdev/) et du [pilote Java MongoDB![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.mongodb.org/ecosystem/drivers/java/), v2.12.3.
* Dans la fonction cloudAutowiring, un bogue qui entraînait des erreurs d'injection de ressources dans certaines applications a été corrigé.

### 3 octobre 2014 : Mise à jour du pack de construction Liberty v1.5-20140923-1143
* Avec le pack de construction mis à jour, les applications peuvent désormais exploiter les fonctions bêta de Liberty, notamment WebSocket 1.0, Servlet 3.1 ou JAX-RS 2.0. pour plus d'informations, voir [Utilisation des fonctions bêta](usingBetaFeatures.html).

### 30 septembre 2014 : Mise à jour du pack de construction Liberty v1.4-20140908-1803
* Le pack de construction assure à présent une prise en charge des services tiers ElephantSQL et ClearDB MySQL Database. La prise en charge de la configuration automatique fonctionne également avec les services expérimentaux posgresql et mysql. Avec un nouveau total de 13 services, la prise en charge de la configuration automatique dans le pack de construction Liberty facilite et accélère l'utilisation de services {{site.data.keyword.Bluemix_notm}} dans les applications Liberty.
* Lors du transfert de l'application, le pack de construction consigne dans le journal des messages améliorés sur la configuration automatique et sur d'autres actions dont il se charge.
* Le pack de construction contient une version mise à jour du profil Liberty avec des correctifs et des améliorations.
* Il contient également une version mise à jour du JRE IBM version 7.1 permettant une amélioration des performances. Pour connaître le détail des modifications, voir la page [Nouveautés](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.71.doc/diag/preface/changes_71/changes.html).

### 28 août 2014 : Mise à jour du pack de construction Liberty v1.3-20140818-1538
* Le pack de construction contient une version mise à jour du [profil Liberty](https://developer.ibm.com/wasdev/) avec des correctifs et des améliorations.
* Cette version du pack de construction adapte la prise en charge de la variable d'environnement JAVA_OPTS afin de transmettre des options JVM supplémentaires à l'environnement d'exécution.
* Elle corrige également un problème empêchant le déploiement d'applications Jar autonomes basées Spring.
* Vous pouvez à présent générer et télécharger des traces snap de la machine virtuelle Java (JVM) IBM à l'aide de l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. Pour en savoir plus sur les traces de snap ou d'autres informations de diagnostic générées par la machine virtuelle Java, voir la rubrique [Troubleshooting](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/troubleshooting.html) dans la documentation de la machine virtuelle Java (JVM) IBM.

### 29 juillet 2014 : Mise à jour du pack de construction Liberty v1.1-20140725-1341
* La nouvelle version de l'édition {{site.data.keyword.Bluemix_notm}} de Liberty est arrivée.
  * Cette version de Liberty inclut des correctifs ainsi que de nouvelles fonctions vous permettant de consommer plus efficacement les services {{site.data.keyword.Bluemix_notm}}.
  * Avec la disponibilité de la nouvelle fonction CouchDB, le service Cloudant peut à présent la configurer automatiquement de manière à disposer rapidement d'un objet connecteur. L'analyse syntaxique de la variable VCAP_SERVICES et la mise à disposition des fichiers JAR de client ektorp ne sont plus nécessaires.
* La nouvelle version d'IBM SDK for Java est arrivée.
  * Lors du prochain envoi par commande push de vos applications, celles-ci utiliseront dorénavant la version 7.1-1.0 d'IBM SDK for Java. Cela se traduit par une amélioration substantielle des performances. Votre application devrait montrer un meilleur débit et utiliser une quantité de mémoire réduite. Pour plus d'informations sur les SDK IBM Java, cliquez [ici](http://www-01.ibm.com/support/docview.wss?uid=swg21671466).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
  * [Environnement d'exécution Liberty](index.html)
  * [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
