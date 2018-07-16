---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 애플리케이션의 모든 페이지에서 HTTPS 강제 실행
{: #enforce_https}

{{site.data.keyword.Bluemix}}에서 애플리케이션을 실행할 때 애플리케이션의 모든 페이지에 HTTP 대신 HTTPS를 강제 실행하려면 애플리케이션에 다음과 같은 변경사항을 적용해야 합니다.

`Startup` 클래스에 다음 `using` 명령문을 추가하십시오.

```
  using Microsoft.AspNetCore.Mvc;
  using Microsoft.AspNetCore.Rewrite;
```

`Startup` 클래스에서 다음 명령문을 `ConfigureServices` 메소드에 추가하십시오.

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

`Startup` 클래스에서 다음 명령문을 `Configure` 메소드에 추가하십시오.

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
