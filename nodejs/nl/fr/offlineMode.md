---

copyright:
  years: 2016, 2018
lastupdated: "2018-07-12"
subcollection: "Nodejs"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Travailler hors ligne avec Node.js
{: #offline_mode}

Quand une application Node.js est envoyée par commande push vers {{site.data.keyword.Bluemix}}, le pack de construction
SDK for Node.js télécharge les artefacts depuis des ressources externes telles que les modules Node de NPM.  Dans certaines situations, par exemple avec [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) et
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), vous pouvez personnaliser l'accès aux sites
externes à {{site.data.keyword.Bluemix_notm}}.  
{: shortdesc}

Le pack de construction Node.js peut accéder aux sites externes suivants. Il est possible que vous deviez *mettre sur liste blanche* ces sites dans les environnements [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) et [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) {{site.data.keyword.Bluemix_notm}}.

* http://nodejs.org/ peut être utilisé pour déterminer les versions du moteur de noeud disponibles.
* https://s3pository.heroku.com sert à extraire les versions du moteur Node non incluses dans le pack de construction.
*  https://www.npmjs.com/package/npm et https://semver.herokuapp.com sont utilisés pour extraire les versions de npm non incluses dans le pack de construction.
* https://iojs.org permet d'extraire une version antérieure d'un noeud qui n'est pas contenue dans le pack de construction ou non disponible sur https://semver.herokuapp.com.
* https://registry.npmjs.org est utilisé pour extraire des modules de noeud comme express.

Pour minimiser l'ensemble de sites mis en liste blanche, configurez vos applications afin qu'elles utilisent une version du moteur Node qui soit incluse dans le pack de construction de SDK for Node.js.  Consultez [Dernières mises à jour](/docs/runtimes/nodejs/updates.html) pour connaître l'ensemble des versions de moteur Node incluses dans le pack de construction.  Si vous configurez votre application de telle sorte qu'elle utilise ces versions de moteur Node, seul le site https://registry.npmjs.org est nécessaire au téléchargement des modules.

Sachez que quand de nouvelles versions du pack de construction de SDK for Node.js sont installées, l'ensemble des versions de moteur est souvent remplacé par un ensemble de versions plus récentes.  Il est possible que vous deviez reconfigurer votre application pour spécifier une version plus récente du moteur Node incluse dans le pack de construction.


## Applications hors ligne
{: #offline_applications}

Pour éliminer le besoin d'accéder à https://registry.npmjs.org, vous pouvez inclure dans votre application tous les modules Node dont cette dernière a besoin.  Pour ce faire, exécutez `npm install` pour tous les modules requis par votre application et incluez le répertoire `node_modules` résultant dans votre application envoyée par commande push.

Vos dépendances peuvent avoir des dépendances qui, elles mêmes, auront des dépendances et ainsi de suite. Cependant, `package.json` ne contient que les dépendances du premier niveau. Si l'une des dépendances utilise une plage de package.json et qu'une nouvelle version de celle-ci est publiée, les modules de votre répertoire `node_modules` peuvent devenir obsolètes. *Shrinkwrap* vous permet de verrouiller toutes les versions de dépendances afin d'empêcher que cela ne se produise.  Pour utiliser shrinkwrap, démarrez avec un répertoire `node_modules` propre ou vide. Ensuite, dans le répertoire racine de votre projet, exécutez les commandes suivantes :

```
npm install
```
{: codeblock}

```
npm dedupe
```
{: codeblock}

```
npm shrinkwrap
```
{: codeblock}

Il est possible que le fichier `package.json` en soit modifié et que le fichier `npm-shrinkwrap.json` soit ajouté à votre répertoire racine.
Dès que vous effectuez un changement dans les dépendances du fichier `package.json`, réexécutez les commandes `npm dedupe` et `shrinkwrap`.

## Utilisation d'un proxy
{: #working_with_proxy}

Dans certains environnements tels que [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) et
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), un proxy peut être configuré. Voir
[Utilisation d'un proxy](/docs/runtimes-common/workingWithProxy.html) pour plus de détails.
