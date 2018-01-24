---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Foire aux questions sur le dépannage
{: #troubleshooting_faq}

**Q** : Le déploiement de mon application échoue avec le message : `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  Qu'est-ce que cela signifie ?

**R** : Si vous recevez un message similaire lors de l'envoi de votre application par commande push, il est fort probable que l'application dépasse les limites de quota de mémoire ou de disque.  Vous pouvez résoudre ce problème en augmentant les quotas pour votre application.

**Q** : Le déploiement de mon application échoue avec le message : `Failed to compress droplet: signal: broken pipe` ou `No space left on device`.  Comment puis-je résoudre ce problème ?

**R** : Les projets poussés à partir d'un code source comprenant de nombreuses dépendances de packages NuGet provoquent parfois cette erreur lorsque la mise en cache des packages NuGet est activée.  Pour désactiver la mise en cache, mettez à `false` la variable d'environnement `CACHE_NUGET_PACKAGES`. Consultez les instructions pour savoir comment [désactiver le package NuGet](diablingNuGet.md) pour plus d'informations.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Présentation d'ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
