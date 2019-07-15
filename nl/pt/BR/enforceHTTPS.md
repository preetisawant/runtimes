---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Impingir HTTPS em todas as páginas em seu aplicativo
{: #enforce_https}

Ao executar seu aplicativo no {{site.data.keyword.Bluemix}} com a estrutura expressa, as mudanças a seguir
precisam ser feitas para impor HTTPS em vez de HTTP em todas as páginas em seu aplicativo.

```
var express = require("express");
var app = express();

app.enable('proxy de confiança');

app.use (function (req, res, next) {
  if (req.secure || process.env.BLUEMIX_REGION === undefined) {
    next();
  } else {
    console.log('redirecionando para https');
    res.redirect('https://' + req.headers.host + req.url);
  }
});
```
