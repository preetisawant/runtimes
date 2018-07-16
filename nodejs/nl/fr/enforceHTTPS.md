---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Imposer l'utilisation de HTTPS sur toutes les pages dans votre application
{: #enforce_https}

Lorsque vous exécutez votre application dans {{site.data.keyword.Bluemix}} avec l'infrastructure Express, les modifications suivantes doivent être effectuées pour imposer l'utilisation de HTTPS au lieu de HTTP sur toutes les pages dans votre application.

```
var express = require("express");
var app = express();

app.enable('trust proxy');

app.use (function (req, res, next) {
  if (req.secure || process.env.BLUEMIX_REGION === undefined) {
    next();
  } else {
    console.log('redirecting to https');
    res.redirect('https://' + req.headers.host + req.url);
  }
});
```
