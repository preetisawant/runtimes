---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


#編譯、發佈及部署應用程式
{: #publish_configure_deploy}

## 在 Release 配置中編譯應用程式（僅限 MSBuild）
{: #compiling_in_release_configuration}

現在，在編譯打包期間，使用 `dotnet publish` 指令來發佈 MSBuild 型專案。建置套件預設會在 `Debug` 配置中發佈應用程式。
若要在 `Release` 配置中發佈應用程式，請將 `PUBLISH_RELEASE_CONFIG` 環境變數設為 `true`。

您可以搭配使用 {{site.data.keyword.Bluemix_notm}} CLI 與下列指令來執行這項作業：

```shell
  ibmcloud cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

或者，您也可以在應用程式的 manifest.yml 檔案中設定此變數：

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## 推送已發佈的應用程式
{: #pushing_published_app}

如果您要應用程式包含其所有必要的二進位檔，讓建置套件不需要下載任何外部二進位檔，則可以推送已發佈的*自行包含* 應用程式。如需自行包含應用程式的相關資訊，請參閱 [.NET Core 應用程式類型](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}。

若要發佈應用程式，請發出指令，例如：
```
dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}

針對自行包含的應用程式，接著可以從
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
目錄推送應用程式。



針對可攜式應用程式，可以從
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
目錄推送應用程式。



也請注意，如果您是在應用程式中使用 manifest.yml 檔案，則可以在 manifest.yml 中指定發佈輸出資料夾的路徑。因此，推送應用程式時，就不需要位在該資料夾中。

## 部署包含多個專案的應用程式
{: #developing_apps_with_multiple_projects}

若要部署包含多個專案的應用程式，則需要指定您要建置套件將哪個專案執行為主要專案。作法是在解決方案的根資料夾中建立可設定主要專案路徑的 .deployment 檔案。主要專案的路徑可以指定為專案資料夾或專案檔（.xproj 或 .csproj）。

例如，如果解決方案在 *src* 資料夾中包含 *MyApp.DAL*、*MyApp.Services* 及 *MyApp.Web* 這三個專案，而且 *MyApp.Web* 是主要專案，則 .deployment 檔案的格式將如下所示：
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

在此範例中，建置套件將自動編譯 *MyApp.DAL* 及 *MyApp.Services* 專案（如果它們列為 *MyApp.Web* 之 project.json 檔案中的相依關係），但建置套件使用 dotnet run -p src/MyApp.Web 時只會嘗試執行主要專案 (*MyApp.Web*)。
