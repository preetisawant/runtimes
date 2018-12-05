---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 复制所需文件以构建输出文件夹
{: #copy_files_build_output}

可以使用 project.json 工具或 MSBuild 工具来确保应用程序在构建输出文件夹中具有其所需的全部文件。
{: shortdesc}


## 使用 project.json 工具
{: #projectjson}

将以下属性添加到 `project.json` 文件的 `buildOptions` 部分中。
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

在 Startup.cs `Startup` 方法中，除去以下行。
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

在 Program.cs `Main` 方法中，除去以下行。
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

这些更改应该可以让 .NET CLI 找到应用程序的 `Views`，因为执行 `dotnet run` 命令之后，这些 Views 将复制到构建输出中。如果应用程序具有在运行时需要的其他任何文件（例如 JSON 配置文件），那么也将这些文件添加到项目的 `project.json` 文件中 `copyToOutput` 的 `include` 部分。

## 使用 MSBuild 工具
{: #msbuild}

将 `<Content>` 元素添加到 `.csproj` 文件的 `<ItemGroup>` 元素中。
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

在 `Startup.cs` `Startup` 方法中，除去以下行。
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

在 `Program.cs` `Main` 方法中，除去以下行。
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

这些更改可以让 .NET CLI 找到应用程序的 `Views`，因为在执行 `dotnet publish` 命令时会将其复制到构建输出中。如果应用程序具有在运行时需要的其他任何文件（例如 JSON 配置文件），那么也将这些文件添加到项目的 .csproj 文件中 `Content` 元素的 `Include` 属性，各文件之间用分号分隔。
