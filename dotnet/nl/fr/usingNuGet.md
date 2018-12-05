---

copyright:
  years: 2015, 2018
lastupdated: "2017-05-31"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Personnalisation des sources de package NuGet
{: #customizing_nuget}

Vous pouvez utiliser le fichier `NuGet.Config` dans le répertoire racine de l'application pour contrôler l'emplacement utilisé par l'application pour télécharger les dépendances. Dans l'exemple suivant, la configuration de la propriété `<packageSources>` définit les clés et les URL d'API permettant à l'application d'extraire les packages.
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}
