---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 必要なファイルのビルド出力フォルダーへのコピー
{: #copy_files_build_output}

project.json ツールまたは MSBuild ツールを使用して、アプリケーションに必要なすべてのファイルがビルド出力フォルダーに入るようにすることができます。
{: shortdesc}


## project.json ツールの使用
{: #projectjson}

`project.json` ファイルの `buildOptions` セクションに以下のプロパティーを追加します。
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

Startup.cs の `Startup` メソッドで、次の行を削除します。
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Program.cs の `Main` メソッドで、次の行を削除します。
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

これらの変更により、.NET CLI がアプリケーションの `Views` を見つけることができます。これは、`dotnet run` コマンドの実行時にビルド出力にコピーされるようになるためです。  JSON 構成ファイルなど、実行時に必要な他のファイルがアプリケーションにある場合、これらのファイルもプロジェクトの `project.json` ファイル内の `copyToOutput` の `include` セクションに追加してください。

## MSBuild ツールの使用
{: #msbuild}

`.csproj` ファイルの `<ItemGroup>` エレメントに `<Content>` エレメントを追加します。
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

`Startup.cs` の `Startup` メソッドで、次の行を削除します。
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

`Program.cs` の `Main` メソッドで、次の行を削除します。
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

これらの変更により、アプリケーションの `Views` は `dotnet publish` コマンドの実行時にビルド出力にコピーされるため、.NET CLI はそれらを見つけることができるようになります。  JSON 構成ファイルなど、実行時に必要な他のファイルがアプリケーションにある場合、これらのファイルも、プロジェクトの .csproj ファイル内の `Content` エレメントの `Include` プロパティーに、セミコロンで区切って追加してください。
