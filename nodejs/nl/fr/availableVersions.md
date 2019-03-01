---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Versions disponibles
{: #available_versions}

{{site.data.keyword.Bluemix}} fournit tous [les environnements d'exécution Node.js disponibles actuellement](http://nodejs.org/dist/). Pour ces environnements d'exécution, {{site.data.keyword.IBM_notm}} fournit des versions spécifiques contenant des améliorations et des correctifs d'erreur. Voir [Dernières mises à jour apportées au pack de construction Node.js](/docs/runtimes/nodejs/updates.html) pour plus d'informations sur les versions prises en charge.
{: shortdesc}

Le pack de construction IBM Node.js met en cache les versions de l'environnement d'exécution {{site.data.keyword.IBM_notm}}. Si vous utilisez l'environnement d'exécution {{site.data.keyword.IBM_notm}} SDK for Node.js dans votre application, cette application s'exécutera plus rapidement lorsque vous l'enverrez par commande push vers {{site.data.keyword.Bluemix_notm}}.

## Spécification d'une version

* Utilisez le paramètre **node** de la section **engines** du fichier **package.json** pour définir la version de l'environnement d'exécution Node.js à exécuter.

* Si vous devez spécifier une version de `npm` différente de la version fournie avec Node.js, utilisez le paramètre `npm` dans la section `engines` du fichier `package.json`.  

Voir l'exemple suivant :

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}

**Remarque :** Indiquez toujours une version de noeud dans le fichier `package.json`. Si aucune version n'est spécifiée, la version de noeud la plus récente est utilisée.
