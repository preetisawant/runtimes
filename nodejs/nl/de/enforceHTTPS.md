---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# HTTPS auf allen Seiten in Ihrer Anwendung erzwingen
{: #enforce_https}

Wenn Sie Ihre Anwendung in {{site.data.keyword.Bluemix}} mit dem Express-Framework ausführen, müssen die folgenden Änderungen vorgenommen werden, um auf allen Seiten Ihrer Anwendung HTTPS anstatt HTTP zu erzwingen.

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
