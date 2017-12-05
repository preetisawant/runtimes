---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Forza HTTPS in tutte le pagine della tua applicazione
{: #enforce_https}

Quando esegui la tua applicazione in Bluemix con il framework express, devono essere effettuate le seguenti modifiche per forzare HTTPS invece di HTTP in tutte le pagine della tua applicazione.

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
