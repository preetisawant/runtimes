---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-25"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 在應用程式的所有頁面上施行 HTTPS
{: #enforce_https}

當您的應用程式在 {{site.data.keyword.Bluemix}} 中執行時，若要在所有頁面上施行 HTTPS 而非 HTTP，您需要對應用程式進行下列變更。

在 `Startup` 類別中新增下列 `using` 陳述式：

```
  using Microsoft.AspNetCore.Mvc;
  using Microsoft.AspNetCore.Rewrite;
```

在 `Startup` 類別中新增下列內容至 `ConfigureServices` 方法：

```
  // if app is running in {{site.data.keyword.Bluemix_notm}}
  if (!string.IsNullOrEmpty(Environment.GetEnvironmentVariable("BLUEMIX_REGION")))
  {
    services.Configure<MvcOptions>(options =>
    {
      options.Filters.Add(new RequireHttpsAttribute());
    });
  }
```

在 `Startup` 類別中新增下列內容至 `Configure` 方法：

```
  // if app is running in {{site.data.keyword.Bluemix_notm}}
  if (!string.IsNullOrEmpty(Environment.GetEnvironmentVariable("BLUEMIX_REGION")))
  {
    app.Use(async (context, next) =>
      {
        if (string.Equals(context.Request.Headers["X-Forwarded-Proto"], "https", StringComparison.OrdinalIgnoreCase))
        {
          context.Request.Scheme = "https";
        }

        await next();
      });
    var options = new RewriteOptions()
                .AddRedirectToHttps();

    app.UseRewriter(options);
  }
```
