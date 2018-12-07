---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Nutzung angepasster nativer Bibliotheken
{: #use_customlib}

Einige Bibliotheken erfordern möglicherweise die Verwendung eines NuGet-Pakets sowie einiger nativer Bibliotheksdateien (Dateien mit der Endung `.so`).  

Zur Verwendung dieser Bibliotheken mit dem Buildpack müssen Sie sie im Ordner `ld_library_path` platzieren, der sich im Stammordner Ihrer Anwendung befindet. Das Buildpack fügt diesen Pfad während des Stagings automatisch der Umgebungsvariablen `LD_LIBRARY_PATH` hinzu.  

Alternativ können Sie die Umgebungsvariable `LD_LIBRARY_PATH` in der Datei `manifest.yml` Ihrer Anwendung angeben oder den Befehl `ibmcloud cf set-env` verwenden, um einen anderen Ordnernamen als `ld_library_path` anzugeben.  In diesem Fall hängt das Buildpack diesen angepassten Pfad an den vom Buildpack generierten `LD_LIBRARY_PATH` an.
