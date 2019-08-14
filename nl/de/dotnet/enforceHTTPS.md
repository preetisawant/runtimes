---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-25"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# HTTPS auf allen Seiten in der Anwendung erzwingen
{: #enforce_https}

Wenn beim Ausführen Ihrer Anwendung in {{site.data.keyword.Bluemix}} auf allen Seiten HTTPS anstatt HTTP erzwungen werden soll, müssen Sie an Ihrer Anwendung die folgenden Änderungen vornehmen.

Fügen Sie die folgenden `using`-Anweisungen in der `Startup`-Klasse hinzu:

```
  using Microsoft.AspNetCore.Mvc;
  using Microsoft.AspNetCore.Rewrite;
```

Fügen Sie der Methode `ConfigureServices` in der `Startup`-Klasse Folgendes hinzu:

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

Fügen Sie der Methode `Configure` in der `Startup`-Klasse Folgendes hinzu:

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
