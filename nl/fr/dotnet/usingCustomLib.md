---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Utilisation de bibliothèques personnalisées
{: #use_customlib}

Il peut être nécessaire d'utiliser à la fois un package NuGet et certaines bibliothèques natives (fichiers `.so`).  

Pour utiliser ces bibliothèques avec le pack de construction, placez-les dans un dossier `ld_library_path` sous le dossier racine de votre application. Le pack de construction ajoute automatiquement ce chemin à la variable d'environnement `LD_LIBRARY_PATH` lors du passage en préproduction (staging).  

Ou bien, vous pouvez spécifier la variable d'environnement `LD_LIBRARY_PATH` dans le fichier `manifest.yml` de votre application ou utiliser la commande `ibmcloud cf set-env` pour spécifier un autre nom de dossier que `ld_library_path`.  Dans ce cas, le pack de construction ajoute le chemin spécifique à la variable `LD_LIBRARY_PATH` qu'il génère.
