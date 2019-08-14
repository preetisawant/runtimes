---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


#Compila, pubblica e distribuisci le applicazioni
{: #publish_configure_deploy}

## Compilazione della tua applicazione nella configurazione della release (solo MSBuild)
{: #compiling_in_release_configuration}

I progetti basati su MSBuild vengono ora pubblicati utilizzando il comando `dotnet publish` durante la fase di preparazione.  Per impostazione predefinita, il pacchetto di build pubblicherà la tua applicazione nella configurazione `Debug`.
Per pubblicare la tua applicazione nella configurazione `Release`, imposta la variabile di ambiente `PUBLISH_RELEASE_CONFIG` su `true`.

Puoi eseguire tale operazione con la CLI {{site.data.keyword.Bluemix_notm}} con il seguente comando:

```shell
  ibmcloud cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

In alternativa, puoi impostare la variabile nel file manifest.yml della tua applicazione:

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## Esecuzione del push di un'applicazione pubblicata
{: #pushing_published_app}

Se desideri che la tua applicazione contenga tutti i propri binari richiesti così che il pacchetto di build non scarichi
binari esterni, puoi eseguire il push di un'applicazione *self-contained* pubblicata.  Consulta
[.NET Core App Types](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}
per ulteriori informazioni sulle applicazioni autonome.

Per pubblicare un'applicazione immetti un comando tipo:
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

Per le applicazioni autonome, l'applicazione può essere trasmessa alla directory
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
.

Per le applicazioni portatili, l'applicazione può essere trasmessa da
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
.

Inoltre tieni presente che se stai utilizzando un file manifest.yml nella tua applicazione, puoi specificare il percorso nella cartella di output di pubblicazione nel tuo manifest.yml.  Quindi non devi essere in tale cartella quando esegui il push dell'applicazione.

## Distribuzione di applicazioni con più progetti
{: #developing_apps_with_multiple_projects}

Per distribuire un'applicazione che contiene più progetti, devi specificare su quale progetto eseguire il pacchetto di build come progetto principale. Ciò può essere eseguito creando un file .deployment nella cartella root della soluzione, che imposti il percorso per il progetto principale. Il percorso al progetto principale può essere specificato come la cartella del progetto o il file del progetto (.xproj o .csproj).

Ad esempio se una soluzione contiene tre progetti, *MyApp.DAL*, *MyApp.Services* e *MyApp.Web* nella cartella *src* e per cui *MyApp.Web* è il progetto principale, il formato del file .deployment deve essere come il seguente:
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

In questo esempio, il pacchetto di build compilerà automaticamente i progetti *MyApp.DAL* e *MyApp.Services* se sono elencati come dipendenze nel file project.json per *MyApp.Web*, ma il pacchetto di build tenterà soltanto di eseguire il progetto principale, *MyApp.Web*, con dotnet run -p src/MyApp.Web.
