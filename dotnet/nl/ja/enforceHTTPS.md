---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# アプリケーションのすべてのページでの HTTPS の適用
{: #enforce_https}

アプリケーションを {{site.data.keyword.Bluemix}} で実行する場合に、アプリケーションのすべてのページで HTTP の代わりに HTTPS を適用するには、アプリケーションに以下の変更を行う必要があります。

`Startup` クラスに以下の `using` ステートメントを追加します。

```
  using Microsoft.AspNetCore.Mvc;
  using Microsoft.AspNetCore.Rewrite;
```

`Startup` クラスの `ConfigureServices` メソッドに以下を追加します。

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

`Startup` クラスの `Configure` メソッドに以下を追加します。

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
