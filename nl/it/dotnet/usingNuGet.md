---

copyright:
  years: 2015, 2018
lastupdated: "2017-05-31"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Personalizza le origini pacchetto NuGet
{: #customizing_nuget}

Puoi utilizzare il file `NuGet.Config` nella directory root dell'applicazione per controllare dove l'applicazione scarica le dipendenze. Nel seguente esempio, configurando la proprietà `<packageSources>` si definiscono tutte le chiavi e gli URL dell'API dell'applicazione per richiamare i pacchetti.
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}
