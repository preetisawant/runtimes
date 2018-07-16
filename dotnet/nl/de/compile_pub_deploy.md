---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


#Anwendungen kompilieren, veröffentlichen und bereitstellen
{: #publish_configure_deploy}

## Anwendung in der Releasekonfiguration kompilieren (nur MSBuild)
{: #compiling_in_release_configuration}

Auf MSBuild basierende Projekte werden jetzt während des Stagings mithilfe des Befehls `dotnet publish` veröffentlicht.  Standardmäßig veröffentlicht das Buildpack Ihre Anwendung in der `Debug`-Konfiguration.
Um Ihre Anwendung in der `Release`-Konfiguration zu veröffentlichen, legen Sie für die Umgebungsvariable `PUBLISH_RELEASE_CONFIG` den Wert `true` fest.

Sie können dies über die {{site.data.keyword.Bluemix_notm}}-CLI mit folgendem Befehl tun:

```shell
  ibmcloud cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

Alternativ können Sie die Variable in der Datei 'manifest.yml' Ihrer Anwendung festlegen:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## Veröffentlichte Anwendung mit einer Push-Operation übertragen
{: #pushing_published_app}

Wenn Sie möchten, dass Ihre Anwendung alle erforderlichen Binärdateien enthält, sodass das Buildpack keine
externen Binärdateien herunterlädt, können Sie eine veröffentlichte *eigenständige* Anwendung mit einer Push-Operation
übertragen.  Weitere Informationen zu eigenständigen Anwendungen finden Sie unter dem Thema [.NET Core App-Typen](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}.

Geben Sie zum Veröffentlichen einer Anwendung einen Befehl wie den folgenden ein:
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

Bei eigenständigen Anwendungen kann die App mit einer Push-Operation aus dem Verzeichnis
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
übertragen werden.

Bei portierbaren Anwendungen kann die App mit einer Push-Operation aus dem Verzeichnis
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
übertragen werden.

Beachten Sie auch, dass Sie, wenn Sie in Ihrer Anwendung eine Datei manifest.yml verwenden, den Pfad des Ausgabeordners 'publish' in Ihrer Datei manifest.yml angeben können.  In diesem Fall müssen Sie sich nicht in diesem Ordner befinden, wenn Sie die Anwendung mit einer Push-Operation übertragen.

## Apps mit mehreren Projekten bereitstellen
{: #developing_apps_with_multiple_projects}

Wenn Sie eine App bereitstellen, die mehrere Projekte enthält, müssen Sie angeben, welches Projekt das Buildpack als Hauptprojekt ausführen soll. Dies kann erfolgen, indem eine .deployment-Datei im Stammordner der Lösung erstellt wird, in der der Pfad für das Hauptprojekt angegeben wird. Der Pfad für das Hauptprojekt kann über den Projektordner oder die Projektdatei (.xproj bzw. .csproj) angegeben werden.

Wenn beispielsweise eine Lösung die drei Projekte *MyApp.DAL*, *MyApp.Services* und *MyApp.Web* im Ordner *src* enthält und *MyApp.Web* das Hauptprojekt ist, würde das Format der .deployment-Datei wie folgt aussehen:
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

In diesem Beispiel würde das Buildpack automatisch die Projekte *MyApp.DAL* und *MyApp.Services* kompilieren, wenn sie in der Datei 'project.json' für *MyApp.Web* als Abhängigkeiten aufgelistet sind, aber das Buildpack würde nur versuchen, das Hauptprojekt, *MyApp.Web*, mit dotnet run -p src/MyApp.Web auszuführen.
