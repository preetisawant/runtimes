---

copyright:
  years: 2015, 2018
lastupdated: "2017-07-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 構成オプション
{: #configuration_options}
{: shortdesc}

## アプリケーションでビルド出力フォルダー内に必要なすべてのファイルが含まれていることの確認
{: #configure_output_files}

### project.json ツールの使用

以下のプロパティーを project.json の `buildOptions` セクションに追加します。
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

これらの変更により、.NET CLI がアプリケーションの `Views` を見つけることができます。これは、`dotnet run` コマンドの実行時にビルド出力にコピーされるようになるためです。  JSON 構成ファイルなど、実行時に必要な他のファイルがアプリケーションにある場合、これらのファイルもプロジェクトの project.json ファイルの `copyToOutput` の `include` セクションに追加する必要があります。

#### MSBuild ツールの使用

以下のように、`<Content>` エレメントを .csproj ファイルの `<ItemGroup>` エレメントに追加します。
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
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

これらの変更により、.NET CLI がアプリケーションの `Views` を見つけることができます。これは、`dotnet publish` コマンドの実行時にビルド出力にコピーされるようになるためです。  JSON 構成ファイルなど、実行時に必要な他のファイルがアプリケーションにある場合、これらのファイルも、セミコロン区切りでプロジェクトの .csproj ファイルの `Content` エレメントの `Include` プロパティーに追加する必要があります。
