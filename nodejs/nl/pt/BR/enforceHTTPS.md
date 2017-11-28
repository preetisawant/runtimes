---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Impingir HTTPS em todas as páginas em seu aplicativo
{: #enforce_https}

Quando você executa seu aplicativo no Bluemix com a estrutura expressa, as mudanças a seguir precisam ser feitas para impingir HTTPS em vez de HTTP em todas as páginas em seu aplicativo.

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
