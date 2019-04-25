---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"
subcollection: "Nodejs"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Utiliser la commande de démarrage
{: #startup_commmand}

Les méthodes recommandées pour spécifier une commande de démarrage pour votre application {{site.data.keyword.Bluemix}} Node.js consistent à utiliser un fichier **Procfile** ou un fichier **package.json**.
{: shortdesc}

1. Pour définir une commande de démarrage dans votre fichier **Procfile**, suivez le modèle ci-dessous. Ici, _app.js_ est le script js de démarrage de votre application.
```
web: node app.js
```
{: codeblock}

1. Sauvegardez le fichier **Procfile** dans le répertoire racine de votre application.

S'il n'existe pas de fichier **Procfile**, le pack de construction Node.js de {{site.data.keyword.Bluemix_notm}} recherche une entrée scripts.start dans le fichier **package.json**. Dans l'exemple ci-dessous, app.js est le script js de démarrage de votre application.
```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

Si une entrée de script de démarrage existe dans le fichier **package.json**, un fichier **Procfile** est généré automatiquement. Le contenu du fichier **Procfile** généré automatiquement est le suivant :
```
    web: npm start
```
{: codeblock}

Pour plus d'informations sur les fichiers **Procfile** et **package.json**, consultez [Tips for Node.js Applications ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).
