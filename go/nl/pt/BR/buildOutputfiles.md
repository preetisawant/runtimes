---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Copie os arquivos necessários para construir a pasta de saída
{: #copy_files_build_output}

É possível usar o conjunto de ferramentas project.json ou MSBuild para assegurar que o aplicativo tenha todos os arquivos necessários na pasta de saída de construção.
{: shortdesc}


## Usar o conjunto de ferramentas project.json
{: #projectjson}

Inclua a seguinte propriedade na seção `buildOptions` do arquivo `project.json`.
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

No método `Startup` de Startup.cs, remova a linha a seguir.
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

No método `Main` de Program.cs, remova a linha a seguir.
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Essas mudanças devem permitir que a CLI .NET localize as `Views`
do seu aplicativo, uma vez que elas agora serão copiadas na saída de construção quando o
comando `dotnet run` for executado.  Se o aplicativo tiver outros arquivos, como os arquivos de configuração JSON, que são necessários no tempo de execução, também inclua-os na seção `include` de `copyToOutput` no arquivo `project.json` para o projeto.

## Usar o conjunto de ferramentas MSBuild
{: #msbuild}

Inclua um elemento `<Content>` no elemento `<ItemGroup>` do arquivo `.csproj`.
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

No método `Startup` de `Startup.cs`, remova a linha a seguir.
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

No método `Main` de `Program.cs`, remove a linha a seguir.
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Essas mudanças permitem que a CLI do .NET localize as `Views` do aplicativo, uma vez que elas são copiadas para a saída de construção quando o comando `dotnet publish` é executado.  Se o aplicativo tiver outros arquivos, como os arquivos de configuração JSON, que são necessários no tempo de execução, também os inclua na propriedade `Include` do elemento `Content` no arquivo .csproj para o projeto, separado por ponto e vírgulas.
