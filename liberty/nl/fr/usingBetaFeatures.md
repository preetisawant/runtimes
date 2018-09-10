---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-10"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utiliser les fonctions bêta
{: #using_beta_features}

Les fonctions bêta de Liberty sont destinées à faciliter l'accès aux nouvelles fonctionnalités et aux nouveaux modèles de programmation pouvant être intégrés dans une édition future de Liberty. La plupart des fonctions bêta peuvent également être utilisées dans des applications déployées sur {{site.data.keyword.Bluemix}}.

**Important** : Les fonctions bêta sont destinées à des fins de développement et de test et ne doivent pas être utilisées en production. Pour connaître les conditions d'utilisation complètes de ces fonctions, voir le document relatif au [contrat de licence des versions bêta](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

| Fonctionnalités |
| ------ |
| `audit-1.0` |
| `logstashCollector-1.1` |
| `mpConfig-1.3` |
| `mpFaultTolerance-1.1` |
| `usageMetering-1.0` |
| `validator-1.0` |
{: caption="Tableau 1. Fonctions bêta Liberty disponibles dans Liberty for Java sous {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

Pour utiliser les fonctions bêta de Liberty dans {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

1. [Déployez un répertoire de serveur ou un package de serveur](optionsForPushing.html) avec une ou plusieurs fonctions bêta activées dans le fichier server.xml, comme dans l'exemple suivant :

  ```
<server>
    <featureManager>
        <feature>usageMetering-1.0</feature>
        <feature>validator-1.0</feature>
    </featureManager>
</server>
  ```
  {: .codeblock}

2.  Mettez à `true` la variable d'environnement `IBM_LIBERTY_BETA`. Cette variable indique au pack de construction Liberty qu'il doit installer et activer les fonctions bêta pour votre application.  Par exemple :
  * Utilisation de l'[interface CLI {{site.data.keyword.Bluemix_notm}} ](../../cli/reference/bluemix_cli/download_cli.html):
    ```
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_BETA true
    ```
    {: .codeblock}

  * Utilisation du fichier `manifest.yml` :
    ```
      env:
          IBM_LIBERTY_BETA: "true"
    ```
    {: .codeblock}

3. Affectez à la variable d'environnement `JBP_CONFIG_LIBERTY` la valeur `"version: +"`. Cette variable active le [contexte d'exécution mensuel Liberty](buildpackDefaults.html#liberty_versions) qui prend en charge les fonctions bêta. Par exemple :
  * Utilisation de l'outil d'interface CLI {{site.data.keyword.Bluemix_notm}} :
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ```
    {: .codeblock}

  * Utilisation du fichier `manifest.yml` :
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
    ```
    {: .codeblock}

Si vous activez les fonctions bêta sur une application existante, n'oubliez pas de reconstituer cette dernière après avoir défini les variables d'environnement.
