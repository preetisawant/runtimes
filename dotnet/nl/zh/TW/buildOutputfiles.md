---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-02"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 複製必要檔案以建置輸出資料夾
{: #copy_files_build_output}

您可以使用 project.json 工具或 MSBuild 工具，以確定應用程式的建置輸出資料夾中具有所有必要檔案。
{: shortdesc}


## 使用 project.json 工具
{: #projectjson}

將下列內容新增至 `project.json` 檔案的 `buildOptions` 區段。
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

在 Startup.cs `Startup` 方法中，移除下列這行。
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

在 Program.cs `Main` 方法中，移除下列這行。
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

這些變更應該容許 .NET CLI 尋找應用程式的 `Views`，因為它們現在會在 `dotnet run` 指令執行時複製到建置輸出。如果您的應用程式具有在執行時需要的任何其他檔案（例如 JSON 配置檔），則也請將檔案新增至專案之 `project.json` 檔案中 `copyToOutput` 的 `include` 區段。

## 使用 MSBuild 工具
{: #msbuild}

將 `<Content>` 元素新增至 `.csproj` 檔案的 `<ItemGroup>` 元素。
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

在 `Startup.cs` `Startup` 方法中，移除下列這行。
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

在 `Program.cs` `Main` 方法中，移除下列這行。
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

這些變更容許 .NET CLI 尋找應用程式的 `Views`，因為它們會在 `dotnet publish` 指令執行時複製到建置輸出。如果您的應用程式具有在執行時需要的任何其他檔案（例如 JSON 配置檔），則也請將檔案新增至專案之 .csproj 檔案中 `Content` 元素的 `Include` 內容，並以分號區隔。
