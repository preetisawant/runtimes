---

copyright:
  years: 2015, 2018
lastupdated: "2017-07-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Opciones de configuración
{: #configuration_options}
{: shortdesc}

## Asegúrese de la aplicación tenga todos los archivos necesarios en la carpeta de salida de la compilación
{: #configure_output_files}

### Utilización de herramientas project.json

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

Estos cambios deben permitir que la CLI de .NET encuentre las `Vistas` de la aplicación porque ahora se copiarán en la salida de la compilación cuando se ejecute el mandato `dotnet run`.  Si la aplicación tiene otros archivos, como los archivos de configuración json, que son necesarios en el tiempo de ejecución, también deberá añadirlos a la sección `include` de `copyToOutput` del archivo project.json correspondiente a su proyecto.

#### Utilización de herramientas MSBuild

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

Estos cambios deben permitir que la CLI de .NET encuentre las `Vistas` de la aplicación porque ahora se copiarán en la salida de la compilación cuando se ejecute el mandato `dotnet publish`.  Si la aplicación tiene otros archivos, como los archivos de configuración json, que son necesarios en el tiempo de ejecución, también deberá añadirlos a la propiedad `Include` del elemento `Content` del archivo project.json correspondiente a su proyecto, separados por signos de punto y coma.
