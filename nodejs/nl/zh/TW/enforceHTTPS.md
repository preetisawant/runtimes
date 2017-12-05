---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 在應用程式的所有頁面上施行 HTTPS
{: #enforce_https}

當您在 Bluemix 中執行應用程式，搭配快速架構時，需要進行下列變更以在應用程式的所有頁面上施行 HTTPS 而非 HTTP。

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
