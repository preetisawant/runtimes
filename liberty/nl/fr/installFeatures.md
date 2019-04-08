---

copyright:
  years: 2018
lastupdated: "2018-12-14"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# Installation de fonctions Liberty
{: #install-features}

L'environnement d'exécution Liberty for Java inclut [un sous-ensemble de fonctions](libertyFeatures.html#liberty_features) disponibles dans Liberty. Vous pouvez installer des fonctions qui ne sont pas incluses dans l'environnement d'exécution en exécutant la commande Liberty `installUtility` en tant que point d'ancrage de pré-exécution Cloud Foundry quand l'application est envoyée par commande push à {{site.data.keyword.cloud_notm}}.

Pour la liste complète des fonctions disponibles, voir [Liberty features ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html).

Pour des informations sur l'utilisation de points d'ancrage de pré-exécution, voir [Configure Pre-Runtime Hooks ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.cloudfoundry.org/devguide/deploy-apps/deploy-app.html#profile) dans la documentation Cloud Foundry.

1. Dans le répertoire racine de l'application à envoyer par commande push à {{site.data.keyword.cloud_notm}}, créez un répertoire `.profile.d`.

1. Dans le répertoire `.profile.d`, créez un fichier script qui exécute la commande `installUtility`, comme illustré dans l'exemple suivant.

   Cet exemple installe la fonction `audit-1.0`.

   ```
   #!/bin/sh
   echo "Installing audit-1.0"
   export PATH=$PATH:$HOME/.java/jre/bin

   $HOME/.liberty/bin/installUtility install audit-1.0 --acceptLicense
   ```
   {: codeblock}

   Vous pouvez installer plusieurs fonctions en spécifiant des noms de fonction supplémentaires, séparés par des espaces.
   {: tip}

1. Envoyez votre application par commande push à {{site.data.keyword.cloud_notm}}, en utilisant le paramètre `-p` pour spécifier le répertoire racine de l'application.

   Exécutez, par exemple, la commande suivante pour envoyer par commande push votre application :
   ```
   ibmcloud cf push myApp -p /<path-to-application>
   ```
   {: codeblock}

1. Vérifiez que la fonction s'est bien installée en affichant le journal récent de l'application.

   Exécutez, par exemple, la commande suivante pour afficher le journal :
   ```
   ibmcloud cf logs myApp --recent
   ```
   {: codeblock}

    Si la fonction est installée, la sortie comporte les messages suivants :

    ```
    2018-09-18T13:01:17.61-0400 [APP/PROC/WEB/0] OUT Installing audit-1.0
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT Establishing a connection to the configured repositories ...
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT This process might take several minutes to complete.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Successfully connected to all configured repositories.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Preparing assets for installation. This process might take several minutes to complete.
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT The --acceptLicense argument was found. This indicates that you have
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT accepted the terms of the license agreement.
    ```
