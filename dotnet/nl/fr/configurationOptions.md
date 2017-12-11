---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Options de configuration
{: #configuration_options}
{: shortdesc}

## Veillez à ce que votre application ait tous les fichiers nécessaires dans le dossier de sortie de construction
{: #configure_output_files}

### Utilisation des outils project.json

Ajoutez la propriété suivante dans la section `buildOptions` du fichier project.json :
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

Dans la méthode `Startup` de Startup.cs, retirez la ligne suivante :
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Dans la méthode `Main` de Program.cs, retirez la ligne suivante :
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Ces changements doivent permettre à .NET CLI de trouver les `Vues` de votre application, car elles sont maintenant copiées dans la sortie de la génération lorsque la commande `dotnet run` est exécutée.  Si votre application a besoin d'autres fichiers au moment de son exécution (par exemple, des fichiers de configuration json), vous devez les ajouter à la section `include` de `copyToOutput` dans le fichier project.json de votre projet.

#### Utilisation des outils MSBuild

Ajoutez un élément `<Content>` à l'élément `<ItemGroup>` de votre fichier .csproj :
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

Dans la méthode `Startup` de Startup.cs, retirez la ligne suivante :
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Dans la méthode `Main` de Program.cs, retirez la ligne suivante :
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Ces changements doivent permettre à .NET CLI de trouver les `Vues` de votre application, car elles sont maintenant copiées dans la sortie de la génération lorsque la commande `dotnet publish` est exécutée.  Si votre application a besoin d'autres fichiers au moment de son exécution (par exemple, des fichiers de configuration json), vous devez aussi les ajouter, en les séparant par des points-virgules, à la propriété `Include` de l'élément `Content` dans le fichier .csproj de votre projet.
