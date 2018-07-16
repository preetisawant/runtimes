---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# アプリケーションのすべてのページでの HTTPS の適用
{: #enforce_https}

Express フレームワークを使用して {{site.data.keyword.Bluemix}} でアプリケーションを実行する場合、アプリケーションのすべてのページで HTTP の代わりに HTTPS を適用するために、以下の変更を行う必要があります。

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
