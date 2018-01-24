---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# FAQ de resolução de problemas
{: #troubleshooting_faq}

**Q**: o aplicativo falha ao implementar com a mensagem: `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  O que isso significa?

**A**: se você estiver recebendo uma mensagem semelhante ao enviar por push seu
aplicativo, provavelmente seu aplicativo está excedendo os limites de cota de memória ou de disco.  Isso pode ser resolvido aumentando as cotas para seu aplicativo.

**Q**: ao ser implementado, meu aplicativo falha com a mensagem: `Falha ao compactar droplet: sinal: canal interrompido` ou `Sem espaço no dispositivo`.  Como posso corrigir isso?

**A**: os projetos enviados por push do código-fonte que contêm um grande número de dependências de pacotes NuGet podem, às vezes, causar esse erro quando o cache de pacote NuGet está ativado.  Configure a variável de ambiente `CACHE_NUGET_PACKAGES` como `false` para desativar o cache. Consulte as instruções sobre como [Desativar o pacote NuGet](diablingNuGet.md) para obter mais informações.

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Visão geral do ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
