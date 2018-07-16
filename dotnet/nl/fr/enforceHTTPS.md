---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Imposer l'utilisation de HTTPS sur toutes les pages dans votre application
{: #enforce_https}

Pour imposer l'utilisation de HTTPS au lieu de HTTP sur toutes les pages dans votre application lorsqu'elle s'exécute dans {{site.data.keyword.Bluemix}}, vous devez lui appliquer les modifications suivantes.

Ajoutez les instructions `using` suivantes dans la classe `Startup` :

```
  using Microsoft.AspNetCore.Mvc;
  using Microsoft.AspNetCore.Rewrite;
```

Ajoutez le code suivant à la méthode `ConfigureServices` dans la classe `Startup` :

```
  // si l'app fonctionne dans {{site.data.keyword.Bluemix_notm}}
  if (!string.IsNullOrEmpty(Environment.GetEnvironmentVariable("BLUEMIX_REGION")))
  {
    services.Configure<MvcOptions>(options =>
    {
      options.Filters.Add(new RequireHttpsAttribute());
    });
  }
```

Ajoutez le code suivant à la méthode `Configure` dans la classe `Startup` :

```
  // si l'app fonctionne dans {{site.data.keyword.Bluemix_notm}}
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
