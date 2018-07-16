---

copyright:
  years: 2015, 2018
lastupdated: "2017-07-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Opções de configuração
{: #configuration_options}
{: shortdesc}

## Assegure-se de que seu aplicativo tenha todos os arquivos necessários na pasta de saída de construção
{: #configure_output_files}

### Usando o conjunto de ferramentas project.json

Inclua a propriedade a seguir na seção `buildOptions` de project.json:
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

No método Startup.cs `Startup`, remova a linha a seguir:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

No método Program.cs `Main`, remova a linha a seguir:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Essas mudanças devem permitir que a CLI .NET localize as `Views`
do seu aplicativo, uma vez que elas agora serão copiadas na saída de construção quando o
comando `dotnet run` for executado.  Se o seu aplicativo tiver quaisquer outros arquivos, como arquivos de configuração json, que são necessários no tempo de execução, também será necessário incluí-los na seção de `include` de `copyToOutput` no arquivo project.json de seu projeto.

#### Usando o conjunto de ferramentas MSBuild

Inclua um elemento `<Content>` no elemento `<ItemGroup>` de seu arquivo .csproj:
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

No método Startup.cs `Startup`, remova a linha a seguir:
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

No método Program.cs `Main`, remova a linha a seguir:
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

Essas mudanças devem permitir que a CLI de .NET localize as `Visualizações` de seu aplicativo, uma vez que elas agora serão copiadas na saída de construção quando o comando `dotnet publish` for executado.  Se o seu aplicativo tiver quaisquer outros arquivos, como arquivos de configuração json, que são necessários no tempo de execução, também será necessário incluí-los na propriedade de `Include` do elemento `Content` no arquivo .csproj de seu projeto, separados por pontos e vírgulas.
