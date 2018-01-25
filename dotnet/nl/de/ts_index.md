---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Fehlerbehebung - Häufig gestellte Fragen (FAQ)
{: #troubleshooting_faq}

**F**: Meine Anwendung schlägt bei der Bereitstellung mit folgender Nachricht fehl: `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  Was bedeutet das?

**A**: Falls Sie eine ähnliche Nachricht erhalten, wenn Sie eine Push-Operation für Ihre Anwendung durchführen, wird dies vermutlich dadurch verursacht, dass Ihre Anwendung entweder den Grenzwert für den Speicher oder für das Datenträgerkontingent überschreitet.  Dieses Problem kann durch Erhöhung der Größenbeschränkung für Ihre Anwendung behoben werden.

**F**: Meine Anwendung schlägt bei der Bereitstellung mit folgender Nachricht fehl: `Failed to compress droplet: signal: broken pipe` oder `No space left on device`.  Wie kann ich den Fehler beheben?

**A**: Projekte, die mit einer Push-Operation von einem Quellcode mit einer großen Anzahl an NuGet-Paketabhängigkeiten übertragen wurden, können diesen Fehler verursachen, wenn der NuGet-Paketcache aktiviert ist.  Legen Sie für die Umgebungsvariable `CACHE_NUGET_PACKAGES` den Wert `false` fest, um das Zwischenspeichern im Cache zu inaktivieren. Weitere Informationen finden Sie in den Anweisungen zum [Inaktivieren des NuGet-Pakets](diablingNuGet.md).

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Übersicht über ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
