---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Preguntas más frecuentes (FAQ) de resolución de problemas
{: #troubleshooting_faq}

**P**: Mi aplicación no se despliega y aparece el mensaje: `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  ¿Qué significa?

**R**: Si recibe un mensaje parecido cuando envía la aplicación, lo más probable es que se deba que la aplicación supera los límites de cuota de memoria o de disco.  Se puede solucionar aumentando las cuotas para la aplicación.

**P**: Mi aplicación no se puede desplegar con el mensaje: `Failed to compress droplet: signal: broken pipe` o `No space left on device`.  ¿Cómo lo puedo solucionar?

**R**: Los proyectos enviados por push desde el código fuente que contienen un gran número de dependencias de paquetes NuGet pueden generar este error cuando la memoria caché de paquetes NuGet está habilitada.  establezca la variable de entorno `CACHE_NUGET_PACKAGES` en `false` para inhabilitar la memoria caché. Para obtener más información, consulte las instrucciones sobre cómo [Inhabilitar el paquete NuGet](diablingNuGet.md).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Visión general de ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
