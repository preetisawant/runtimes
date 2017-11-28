---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Impingir HTTPS em todas as páginas em seu aplicativo
{: #enforce_https}

Para impingir HTTPS em vez de HTTP em todas as páginas em seu aplicativo quando ele é executado no Bluemix, é necessário fazer as mudanças a seguir em seu aplicativo.

Inclua as instruções `using` a seguir na classe `Startup`:

```
  using Microsoft.AspNetCore.Mvc;
  using Microsoft.AspNetCore.Rewrite;
```

Inclua o seguinte no método `ConfigureServices` na classe `Startup`:

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

Inclua o seguinte no método `Configure` na classe `Startup`:

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
