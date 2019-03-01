---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Node.js
{: #nodejs_runtime}

L'environnement d'exécution Node.js sur {{site.data.keyword.Bluemix}} utilise la technologie du pack de construction sdk-for-nodejs.
Le pack de construction sdk-for-nodejs fournit un environnement d'exécution complet pour les applis Node.js.
{: shortdesc}

Le pack de construction sdk-for-nodejs est utilisé lorsque l'application contient un fichier **package.json** dans le répertoire racine.

L'application doit écouter sur le port qui lui est affecté via la variable d'environnement PORT.
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} contient une application de démarrage Node.js.  L'application de démarrage Node.js est une appli Node.js simple qui peut servir de modèle pour votre appli. Vous pouvez l'utiliser pour faire des essais, faire des modifications et les envoyer par commande push vers l'environnement {{site.data.keyword.Bluemix_notm}}. Consultez [Utilisation des applications de démarrage](/docs/runtimes-common/starter_app_usage.html) pour obtenir de l'aide sur l'application de démarrage.

## App Management
{: #app_management}
{{site.data.keyword.Bluemix_notm}} fournit un certain nombre d'utilitaires pour la gestion et le débogage de l'appli Node.js. Pour plus de détails, voir [App Management](/docs/runtimes-common/app_mng.html).
