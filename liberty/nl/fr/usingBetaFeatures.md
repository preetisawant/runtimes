---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utiliser les fonctions bêta
{: #using_beta_features}

Les fonctions bêta de Liberty sont destinées à faciliter l'accès aux nouvelles fonctionnalités et aux nouveaux modèles de programmation pouvant être intégrés dans une édition future de Liberty. La plupart des fonctions bêta peuvent également être utilisées dans des applications déployées sur {{site.data.keyword.Bluemix}}.

**Important** : Les fonctions bêta sont destinées à des fins de développement et de test et ne doivent pas être utilisées en
production. Pour connaître les conditions d'utilisation complètes de ces fonctions, voir le document relatif au [contrat de licence des versions bêta](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

Fonctions bêta de Liberty disponibles dans {{site.data.keyword.Bluemix_notm}}
<table>
<tr>
<th align="left">Fonctionnalités</th>
</tr>

<tr>
    <tr><td>appSecurity-3.0</tr></td>
    <tr><td>audit-1.0</tr></td>
    <tr><td>beanValidation-2.0</tr></td>
    <tr><td>bluemixLogCollector-1.1</tr></td>
    <tr><td>cdi-2.0</tr></td>
    <tr><td>javaee-8.0</tr></td>
    <tr><td>javaeeClient-8.0</tr></td>
    <tr><td>jaxrs-2.1</tr></td>
    <tr><td>jpa-2.2</tr></td>
    <tr><td>jpaContainer-2.2</tr></td>
    <tr><td>jsf-2.3</tr></td>
    <tr><td>jsfContainer-2.2</tr></td>
    <tr><td>jsonb-1.0</tr></td>
    <tr><td>jsonbContainer-1.0</tr></td>
    <tr><td>jsonp-1.1</tr></td>
    <tr><td>jsonpContainer-1.1</tr></td>
    <tr><td>logstashCollector-1.1</tr></td>
    <tr><td>mpConfig-1.2</tr></td>
    <tr><td>mpOpenAPI-1.0</tr></td>
    <tr><td>mpRestClient-1.0</tr></td>
    <tr><td>opentracing-1.0</tr></td>
    <tr><td>servlet-4.0</tr></td>
    <tr><td>validator-1.0</tr></td>
    <tr><td>webProfile-8.0</tr></td>

</tr>
</table>

Pour utiliser les fonctions bêta de Liberty dans {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

1. [Déployez un répertoire de serveur ou un package de serveur](optionsForPushing.html) avec une ou plusieurs fonctions bêta activées dans le fichier server.xml, comme dans l'exemple suivant :
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>mpOpenAPI-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Mettez à **true** la variable d'environnement **IBM_LIBERTY_BETA**. Cette variable indique au pack de construction Liberty qu'il doit installer et activer les fonctions bêta pour votre application.  Par exemple :
  * Utilisation de l'outil de ligne de commande cf :
```
       $ cf set-env <yourappname> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * Ou, utilisation du fichier manifest.yml :
```
      env:
          IBM_LIBERTY_BETA: "true"
```

3. Affectez à la variable d'environnement **JBP_CONFIG_LIBERTY** la valeur **"version: +"**. Cette variable active le [contexte d'exécution mensuel Liberty](buildpackDefaults.html#liberty_versions) qui prend en charge les fonctions bêta. Par exemple :
  * Utilisation de l'outil de ligne de commande cf :
```
       $ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * Ou, utilisation du fichier manifest.yml :
```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
```

Si vous activez les fonctions bêta sur une application existante, n'oubliez pas de reconstituer cette dernière après avoir défini les variables d'environnement.

{: #codeblock}

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Exécution de Liberty for Java](index.html)
* [Présentation de Liberty](https://www.ibm.com/support/knowledgecenter/SSAW57_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/cwlp_about.html)
