---

copyright:
  years: 2015, 2018
lastupdated: "2017-05-31"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Informationen zum Anpassen von NuGet-Paketquellen
{: #customizing_nuget}
Mit der Datei NuGet.Config im Stammverzeichnis der Anwendung können Sie die Quellen steuern, die von der Anwendung zum Herunterladen von Abhängigkeiten verwendet werden. Im folgenden Beispiel werden durch das Konfigurieren der Eigenschaft `<packageSources>` sämtliche Schlüssel und API-URLs zum Abrufen von Paketen für die Anwendung definiert.
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}
