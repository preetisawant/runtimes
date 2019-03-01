---

copyright:
  years: 2019
lastupdated: "2019-02-01"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utiliser l'exécution mensuelle
{: #using_monthly_runtime}

L'exécution mensuelle de Liberty fournit la version la plus récente ainsi que l'accès aux nouveaux modèles de programmation et fonctionnalités.

Pour utiliser l'exécution mensuelle de Liberty dans {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

Définissez la variable d'environnement `JBP_CONFIG_LIBERTY` sur `"version: +"` et la variable d'environnement `IBM_LIBERTY_MONTHLY` sur `true`. Ces variables activent l'[exécution mensuelle de Liberty](/docs/runtimes/liberty/buildpackDefaults.html#liberty_versions). Par exemple :
  * Utilisation de l'outil d'interface CLI {{site.data.keyword.Bluemix_notm}} :
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_MONTHLY true
    ```
    {: .codeblock}

  * Utilisation du fichier `manifest.yml` :
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
          IBM_LIBERTY_MONTHLY: true
    ```

    ```
      env:
          JBP_CONFIG_LIBERTY: "[version: +, app_archive: {features: [javaee-8.0]}]"
          IBM_LIBERTY_MONTHLY: true
    ```
    {: .codeblock}

Si vous activez l'exécution mensuelle sur une application existante, vous devrez peut-être supprimer puis envoyer à nouveau par commande push votre application après avoir défini les variables d'environnement.
