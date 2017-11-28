---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Domande frequenti (FAQ) sulla risoluzione dei problemi
{: #troubleshooting_faq}

**Q**: la mia applicazione non può distribuire il messaggio: `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  Cosa significa?

**A**: se stai ricevendo un messaggio simile quando esegui il push della tua applicazione, molto probabilmente la tua applicazione sta superando i limiti della quota di memoria o del disco.  Questo problema può essere risolto incrementando le quote della tua applicazione.

**Q**: impossibile eseguire la distribuzione della mia applicazione con il messaggio di errore: `Impossibile comprimere il droplet: segnale: pipe interrotta` o `Mancanza di spazio sul dispositivo`.  In che modo è possibile correggere l'errore?

**A**: i progetti trasmessi dal codice di origine che contiene una grande numero di dipendenze del pacchetto NuGet può a volte causare questo errore quando viene abilitata la cache del pacchetto NuGet.  Imposta la variabile di ambiente `CACHE_NUGET_PACKAGES` su `false` per disabilitare la cache. Per ulteriori informazioni, consulta le istruzioni su come [Disabilitare il pacchetto NuGet](diablingNuGet.md).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Panoramica ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
