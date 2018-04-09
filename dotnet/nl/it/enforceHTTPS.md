---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Forza HTTPS in tutte le pagine della tua applicazione
{: #enforce_https}

Per forzare HTTPS invece di HTTP in tutte le pagine della tua applicazione quando viene eseguita in {{site.data.keyword.Bluemix}}, devi effettuare le seguenti modifiche alla tua applicazione.

Aggiungi le seguenti istruzioni `using` nella casse `Startup`:

```
  using Microsoft.AspNetCore.Mvc;
  using Microsoft.AspNetCore.Rewrite;
```

Aggiungi quanto segue al metodo `ConfigureServices` nella classe `Startup`:

```
  // se l'applicazione è in esecuzione in {{site.data.keyword.Bluemix_notm}}
  if (!string.IsNullOrEmpty(Environment.GetEnvironmentVariable("BLUEMIX_REGION")))
  {
    services.Configure<MvcOptions>(options =>
    {
      options.Filters.Add(new RequireHttpsAttribute());
    });
  }
```

Aggiungi quanto segue al tuo metodo `Configure` nella classe `Startup`:

```
  // se l'applicazione è in esecuzione in {{site.data.keyword.Bluemix_notm}}
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
