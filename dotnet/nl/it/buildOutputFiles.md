---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Copia i file necessari per creare la cartella di output
{: #copy_files_build_output}

Puoi utilizzare la strumentazione project.json oppure la strumentazione MSBuild per garantire che la tua applicazione abbia tutti i suoi file necessari nella cartella di output della build.
{: shortdesc}


## Utilizza lo strumento project.json
{: #projectjson}

Aggiungi la seguente proprietà alla sezione `buildOptions` del file `project.json`.
```
  "copyToOutput": {
    "include": [
      "wwwroot",
      "Areas/**/Views",
      "Views",
      "appsettings.json"
    ]
  }
```
{: codeblock}

Nel metodo `Startup` Startup.cs, rimuovi la seguente riga.
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Nel metodo `Main` Program.cs, rimuovi la seguente riga.
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Queste modifiche consentono alla CLI .NET di trovare le `Views` della tua applicazione che saranno ora copiate nell'output di build quando viene eseguito il comando `dotnet run`.  Se la tua applicazione ha degli altri file, come ad esempio dei file di configurazione JSON, che sono necessari al runtime, aggiungi i file anche alla sezione `include` di `copyToOutput` nel file `project.json` per il tuo progetto.

## Utilizza lo strumento MSBuild
{: #msbuild}

Aggiungi un elemento `<Content>` all'elemento `<ItemGroup>` del tuo file `.csproj`.
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

Nel metodo `Startup.cs` `Startup`, rimuovi la seguente riga.
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Nel metodo `Program.cs` `Main`, rimuovi la seguente riga.
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Queste modifiche consentono alla CLI .NET di trovare le `Views` della tua applicazione poiché vengono copiate nell'output di build quando viene eseguito il comando `dotnet publish`.  Se la tua applicazione dispone di altri file, come ad esempio dei file di configurazione JSON, che sono necessari al runtime, aggiungi anche tali file alla proprietà `Include` dell'elemento `Content` nel file .csproj del tuo progetto, separati da caratteri punto e virgola.
