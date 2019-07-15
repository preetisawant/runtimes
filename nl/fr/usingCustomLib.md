---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# A propos des bibliothèques personnalisées
{: #use_customlib}

{: #shortdesc}

## Utilisation de bibliothèques natives personnalisées
{: #using_custom_native_libraries}

Il est parfois nécessaire d'utiliser à la fois un package NuGet et certaines bibliothèques natives (fichiers .so).  Pour que ces bibliothèques soient utilisables avec le pack de construction, vous devez les placer dans un dossier nommé *ld_library_path* sous le dossier racine de votre application.
Le pack de construction ajoutera automatiquement ce chemin à la variable d'environnement `LD_LIBRARY_PATH` lors du passage en préproduction (staging).  Ou bien, vous pouvez spécifier la variable d'environnement `LD_LIBRARY_PATH` dans le fichier `manifest.yml` de votre application ou utiliser la commande `ibmcloud cf set-env` pour spécifier un autre nom de dossier que *ld_library_path*.  Dans ce cas, le pack de construction ajoutera le chemin spécifique à la variable `LD_LIBRARY_PATH` qu'il générera.
