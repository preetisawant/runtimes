---

copyright:
  years: 2015, 2018
lastupdated: "2017-08-10"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 필요한 파일을 빌드 출력 폴더에 복사
{: #copy_files_build_output}

project.json 도구 또는 MSBuild 도구를 사용하여 애플리케이션에 빌드 출력 폴더에 필요한 모든 파일이 있는지 확인할 수 있습니다.
{: #shortdesc}


## project.json 도구 사용

project.json의 `buildOptions` 섹션에 다음 특성을 추가하십시오.
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

Startup.cs `Startup` 메소드에서 다음 행을 제거하십시오.
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Program.cs `Main` 메소드에서 다음 행을 제거하십시오.
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

이렇게 변경하면 .NET CLI가 애플리케이션의 `Views`를 찾을 수 있게 됩니다. 이제 이러한 보기가 `dotnet run` 명령이 실행될 때 빌드 출력에 복사되기 때문입니다.  애플리케이션에 런타임 시 필요한 다른 파일(예: json 구성 파일)이 있는 경우에는 이러한 파일도 프로젝트의 project.json 파일에 있는 `copyToOutput`의 `include` 섹션에 추가해야 합니다.

## MSBuild 도구 사용

`<Content>` 요소를 .csproj 파일의 `<ItemGroup>` 요소에 추가하십시오.
```
  <ItemGroup>
    <Content Include="wwwroot/**/*;Areas/**/Views/*;Views/*;appsettings.json">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
      <CopyToPublishDirectory>Always</CopyToPublishDirectory>
    </Content>
  </ItemGroup>
```
{: codeblock}

Startup.cs `Startup` 메소드에서 다음 행을 제거하십시오.
```
  .SetBasePath(env.ContentRootPath)
```
{: codeblock}

Program.cs `Main` 메소드에서 다음 행을 제거하십시오.
```
  .UseContentRoot(Directory.GetCurrentDirectory())
```
{: codeblock}

이렇게 변경하면 .NET CLI가 애플리케이션의 `Views`를 찾을 수 있게 됩니다. 이제 이러한 보기가 `dotnet publish` 명령이 실행될 때 빌드 출력에 복사되기 때문입니다.  애플리케이션에 런타임 시 필요한 다른 파일(예: json 구성 파일)이 있는 경우에는 이러한 파일도 프로젝트의 .csproj 파일에 있는 `Content` 요소의 `Include` 특성에 추가해야 하며, 세미콜론으로 구분합니다.
