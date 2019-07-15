---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


#애플리케이션 컴파일, 공개 및 배치
{: #publish_configure_deploy}

## 릴리스 구성의 애플리케이션 컴파일(MSBuild에만 해당)
{: #compiling_in_release_configuration}

MSBuild 기반 프로젝트는 스테이징 중에 `dotnet publish` 명령을 사용하여 공개됩니다.  기본적으로 빌드팩은 `Debug` 구성의 애플리케이션을 공개합니다.
`Release` 구성의 애플리케이션을 공개하려면 `PUBLISH_RELEASE_CONFIG` 환경 변수를 `true`로 설정하십시오.

다음 명령을 사용하여 {{site.data.keyword.Bluemix_notm}} CLI에서 이를 수행할 수 있습니다.

```shell
  ibmcloud cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

또는 애플리케이션의 manifest.yml 파일에서 변수를 설정할 수 있습니다.

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## 공개된 애플리케이션 푸시
{: #pushing_published_app}

빌드팩이 외부 바이너리를 다운로드하지 않도록 애플리케이션이 모든 필수 바이너리를 포함하게 하려는 경우,
공개된 *자체 포함* 애플리케이션을 푸시할 수 있습니다.  자체 포함 애플리케이션에 대한 자세한 정보는
[.NET Core 앱 유형](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}을 참조하십시오.

애플리케이션을 공개하려면 다음과 같이 명령을 발행하십시오.
```
  dotnet publish -r ubuntu.14.04-x64
```
{: codeblock}

자체 포함된 애플리케이션의 경우 앱을 다음 디렉토리에서 푸시할 수 있습니다.
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}


휴대용 애플리케이션의 경우 앱을 다음 디렉토리에서 푸시할 수 있습니다.
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}


또한 애플리케이션에서 manifest.yml 파일을 사용 중인 경우 manifest.yml에 공개 출력 폴더에 대한 경로를 지정할 수 있음을 참고하십시오.  그런 다음에는 애플리케이션을 푸시할 때 해당 폴더 내에 있지 않아도 됩니다.

## 다중 프로젝트가 있는 앱의 배치
{: #developing_apps_with_multiple_projects}

다중 프로젝트를 포함하는 앱을 배치하려면 빌드팩을 기본 프로젝트로 실행할 프로젝트를 지정해야 합니다. 이는 기본 프로젝트에 대한 경로를 설정하는 솔루션의 루트 폴더에 배치 파일을 작성하여 수행할 수 있습니다. 기본 프로젝트에 대한 경로는 프로젝트 폴더 또는 프로젝트 파일(.xproj 또는 .csproj)로 지정될 수 있습니다.

예를 들어 세 개의 프로젝트, *MyApp.DAL*, *MyApp.Services*, *MyApp.Web*을 *src* 폴더에 포함하고 *MyApp.Web*이 기본 프로젝트인 솔루션의 경우 배치 파일의 형식은 다음과 같습니다.
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

이 예제에서, *MyApp.DAL* 및 *MyApp.Services* 프로젝트가 *MyApp.Web*용 project.json 파일의 종속 항목으로 나열된 경우에 빌드팩은 자동으로 이 프로젝트들을 컴파일하지만 실행은 기본 프로젝트인 *MyApp.Web*에 대해서만 dotnet run -p src/MyApp.Web을 사용하여 시도합니다.
