---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-02"

subcollection: "dotnet"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Copier les fichiers requis pour générer le dossier de sortie
{: #copy_files_build_output}

Vous pouvez utiliser les outils project.json ou MSBuild pour garantir que votre application comporte tous les fichiers requis dans le dossier de sortie généré.
{: shortdesc}


## Utiliser les outils project.json
{: #projectjson}

Ajoutez la propriété suivante dans la section `buildOptions` du fichier `project.json`.
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

Dans la méthode `Startup` de Startup.cs, retirez la ligne suivante.
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Dans la méthode `Main` de Program.cs, retirez la ligne suivante.
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Ces changements doivent permettre à .NET CLI de trouver les `Vues` de votre application, car elles sont maintenant copiées dans la sortie de la génération lorsque la commande `dotnet run` est exécutée.  Si votre application a besoin d'autres fichiers au moment de son exécution (par exemple, des fichiers de configuration JSON), vous devez les ajouter à la section `include` de `copyToOutput` dans le fichier `project.json` de votre projet.

## Utiliser les outils MSBuild
{: #msbuild}

Ajoutez un élément `<Content>` à l'élément `<ItemGroup>` de votre fichier `.csproj`.
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

Dans la méthode `Startup.cs` `Startup`, retirez la ligne suivante.
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Dans la méthode `Program.cs` `Main`, retirez la ligne suivante.
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Ces changements permettent à .NET CLI de trouver les `Vues` de votre application, car elles sont maintenant copiées dans la sortie de la génération lorsque la commande `dotnet publish` est exécutée.  Si votre application a besoin d'autres fichiers au moment de son exécution (par exemple, des fichiers de configuration JSON), ajoutez-les également, en les séparant par des points-virgules, à la propriété `Include` de l'élément `Content` dans le fichier .csproj de votre projet.
