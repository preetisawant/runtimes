---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-10"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Copiar los archivos necesarios en la carpeta de salida de la compilación
{: #copy_files_build_output}

Puede utilizar las herramientas project.json o MSBuild para asegurarse de que la aplicación tenga todos los archivos necesarios en la carpeta de salida de la compilación.
{: #shortdesc}


## Utilizar las herramientas project.json

Añada la siguiente propiedad a la sección `buildOptions` de project.json:
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

En el método `Startup` de Startup.cs, elimine la siguiente línea:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

En el método `Main` de Program.cs, elimine la siguiente línea:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Estos cambios deben permitir que .NET CLI encuentre las `Views` de la aplicación porque ahora se copiarán en la salida de la compilación cuando se ejecute el mandato `dotnet run`.  Si la aplicación tiene otros archivos, como los archivos de configuración json, que son necesarios en el tiempo de ejecución, también deberá añadirlos a la sección `include` de `copyToOutput` del archivo project.json correspondiente a su proyecto.

## Utilizar herramientas MSBuild

Agregue un elemento `<Content>` al elemento `<ItemGroup>` del archivo .csproj:
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

En el método `Startup` de Startup.cs, elimine la siguiente línea:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

En el método `Main` de Program.cs, elimine la siguiente línea:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Estos cambios deben permitir que .NET CLI encuentre las `Views` de la aplicación porque ahora se copiarán en la salida de la compilación cuando se ejecute el mandato `dotnet publish`.  Si la aplicación tiene otros archivos, como los archivos de configuración json, que son necesarios en el tiempo de ejecución, también deberá añadirlos a la propiedad `Include` del elemento `Content` del archivo project.json correspondiente a su proyecto, separados por signos de punto y coma.
