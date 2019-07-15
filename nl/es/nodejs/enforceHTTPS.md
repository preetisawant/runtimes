---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Aplicar HTTPS en todas las páginas de la aplicación
{: #enforce_https}

Cuando se ejecuta la aplicación en {{site.data.keyword.Bluemix}} con la infraestructura de Express, es necesario realizar los cambios siguientes para aplicar HTTPS en lugar de HTTP en todas las páginas de la aplicación.

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
