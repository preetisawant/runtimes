---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 애플리케이션의 모든 페이지에서 HTTPS 강제 실행
{: #enforce_https}

Express 프레임워크를 사용하여 {{site.data.keyword.Bluemix}}에서 애플리케이션을 실행할 때 애플리케이션의 모든 페이지에서 HTTP 대신 HTTPS를 강제 실행하려면 다음과 같이 변경해야 합니다.

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
