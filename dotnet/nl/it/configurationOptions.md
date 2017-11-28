---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Opzioni di configurazione 
{: #configuration_options}
{: shortdesc}

## Assicurati che la tua applicazione abbia tutti i file necessari nella cartella di output della build.
{: #configure_output_files}

### Utilizzo dello strumento project.json

Aggiungi la seguente proprietà alla sezione `buildOptions` di project.json:
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

Nel metodo `Startup` Startup.cs, rimuovi la seguente riga:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Nel metodo `Main` Program.cs, rimuovi la seguente riga:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Queste modifiche consentono alla CLI .NE di trovare le `Views` della tua applicazione che saranno ora copiate nell'output di build quando viene eseguito il comando `dotnet run`.  Se la tua applicazione dispone di altri file, come ad esempio dei file di configurazione json, richiesti durante il runtime, devi quindi aggiungerli nella sezione `include` di `copyToOutput` nel file project.json del tuo progetto.

#### Utilizzo dello strumento MSBuild

Aggiungi un elemento `<Content>` all'elemento `<ItemGroup>` del tuo file .csproj:
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

Nel metodo `Startup` Startup.cs, rimuovi la seguente riga:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Nel metodo `Main` Program.cs, rimuovi la seguente riga:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Queste modifiche consentono alla CLI .NE di trovare le `Views` della tua applicazione che saranno ora copiate nell'output di build quando viene eseguito il comando `dotnet publish`.  Se la tua applicazione dispone di altri file, come ad esempio dei file di configurazione json, richiesti durante il runtime, devi quindi aggiungerli nella proprietà `Include` dell'elemento `Content` nel file .csproj del tuo progetto, separati da punti e virgola.
