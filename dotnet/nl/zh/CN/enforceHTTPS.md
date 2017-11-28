---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 在应用程序的所有页面上强制实施 HTTPS
{: #enforce_https}

当应用程序在 Bluemix 上运行时，要在所有页面上强制实施 HTTPS 而非 HTTP，需要对应用程序进行如下更改。

在 `Startup` 类中添加以下 `using` 语句：

```
  using Microsoft.AspNetCore.Mvc;
  using Microsoft.AspNetCore.Rewrite;
```

在 `Startup` 类中将以下内容添加到 `ConfigureServices` 方法：

```
  // if app is running in Bluemix
  if (!string.IsNullOrEmpty(Environment.GetEnvironmentVariable("BLUEMIX_REGION")))
  {
    services.Configure<MvcOptions>(options =>
    {
      options.Filters.Add(new RequireHttpsAttribute());
    });
  }
```

在 `Startup` 类中将以下内容添加到 `Configure` 方法：

```
  // if app is running in Bluemix
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
