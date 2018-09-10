---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Informationen zu angepassten Bibliotheken
{: #use_customlib}

{: #shortdesc}

## Angepasste native Bibliotheken verwenden
{: #using_custom_native_libraries}

Einige Bibliotheken erfordern möglicherweise die Verwendung eines NuGet-Pakets sowie einiger nativer Bibliotheksdateien (.so-Dateien).  Um diese Bibliotheken mit dem Buildpack zu verwenden, sollten Sie sie in einen Ordner mit dem Namen *ld_library_path* in den Stammordner Ihrer Anwendung stellen.
Das Buildpack fügt diesen Pfad während des Stagings automatisch der Umgebungsvariablen `LD_LIBRARY_PATH` hinzu.  Alternativ können Sie die Umgebungsvariable `LD_LIBRARY_PATH` in der Datei `manifest.yml` Ihrer Anwendung angeben oder den Befehl `ibmcloud cf set-env` verwenden, um einen anderen Ordnernamen als *ld_library_path* anzugeben.  In diesem Fall hängt das Buildpack diesen angepassten Pfad an den vom Buildpack generierten `LD_LIBRARY_PATH` an.
