---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Exécuter l'application Node.js localement
{: #hints}

Choisissez un numéro de port permettant à votre application Node.js de fonctionner localement sans pour autant provoquer de conflit lorsqu'elle sera ensuite exécutée sur {{site.data.keyword.Bluemix}}.
{: shortdesc}

Lorsque l'application fonctionne sur {{site.data.keyword.Bluemix_notm}}, la variable d'environnement PORT est allouée par Cloud Foundry. En revanche, lorsque l'application est exécutée localement, la variable PORT n'est pas définie et vous êtes donc libre de définir vous-même le port que doit écouter l'application. Pour éviter tout conflit, choisissez un numéro de port différent de celui qui sera utilisé par {{site.data.keyword.Bluemix_notm}}.

Dans l'exemple suivant, pour un fichier **js**, le numéro de port **3000** est utilisé. En utilisant **3000**, vous pouvez exécuter l'application localement pour vos tests, puis sur {{site.data.keyword.Bluemix_notm}} sans avoir besoin de changer quoi que ce soit.

```
var port = (process.env.PORT || 3000);
```
{: codeblock}
