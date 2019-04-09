---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-02"

subcollection: "dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Copiar los archivos necesarios en la carpeta de salida de la compilación
{: #copy_files_build_output}

Puede utilizar las herramientas project.json o MSBuild para asegurarse de que la aplicación tenga todos los archivos necesarios en la carpeta de salida de la compilación.
{: shortdesc}


## Utilizar las herramientas project.json
{: #projectjson}

Añada la siguiente propiedad a la sección `buildOptions` del archivo `project.json`.
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

En el método `Startup` de Startup.cs, elimine la siguiente línea.
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

En el método `Main` de Program.cs, elimine la siguiente línea.
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Estos cambios deben permitir que la CLI de .NET encuentre las `Vistas` de la aplicación porque ahora se copiarán en la salida de la compilación cuando se ejecute el mandato `dotnet run`.  Si la aplicación tiene otros archivos, como los archivos de configuración JSON, que son necesarios en el tiempo de ejecución, también deberá añadirlos a la sección `include` de `copyToOutput` del archivo `project.json` correspondiente a su proyecto.

## Utilizar herramientas MSBuild
{: #msbuild}

Agregue un elemento `<Content>` al elemento `<ItemGroup>` del archivo `.csproj`.
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

En el método `de inicio` `Startup.cs`, elimine la siguiente línea.
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

En el método `principal` `Program.cs`, elimine la siguiente línea.
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Estos cambios permiten que .NET CLI encuentre las `Vistas` de la aplicación porque se copian en la salida de la compilación cuando se ejecute el mandato `dotnet publish`.  Si la aplicación tiene otros archivos, como los archivos de configuración JSON, que son necesarios en el tiempo de ejecución, añádalos a la propiedad `Include` del elemento `Content` del archivo project.json correspondiente a su proyecto, separados por signos de punto y coma.
