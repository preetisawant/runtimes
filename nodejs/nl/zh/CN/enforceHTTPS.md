---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 在应用程序的所有页面上强制实施 HTTPS
{: #enforce_https}

当使用 Express 框架在 Bluemix 中运行应用程序时，需要做以下更改以在应用程序的所有页面上强制实施 HTTPS 而不是 HTTP。

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
