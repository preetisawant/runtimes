---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-31"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


#编译、发布、部署应用程序
{: #publish_configure_deploy}

## 在 Release 配置中编译应用程序（仅限 MSBuild）
{: #compiling_in_release_configuration}

现在，基于 MSBuild 的项目在编译打包期间使用 `dotnet publish` 命令发布。缺省情况下，buildpack 将在 `Debug` 配置中发布应用程序。
要在 `Release` 配置中发布应用程序，请将 `PUBLISH_RELEASE_CONFIG` 环境变量设置为 `true`。

可以通过 Cloud Foundry CLI 使用以下命令来执行此操作：

```shell
  cf set-env <app_name> PUBLISH_RELEASE_CONFIG true
```

或者，可以在应用程序的 manifest.yml 文件中设置此变量：

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    PUBLISH_RELEASE_CONFIG: true
```

## 推送发布的应用程序
{: #pushing_published_app}

如果想要在应用程序中包含其需要的所有二进制文件，以使 buildpack 无需下载任何外部二进制文件，您可以推送发布的*自包含*应用程序。请参阅 [.NET Core App Types](https://docs.microsoft.com/en-us/dotnet/articles/core/app-types){: new_window}，以获取有关自包含应用程序的更多信息。

要发布应用程序，请发出类似如下命令：
```
dotnet publish -r ubuntu.14.04-x64 
```
{: codeblock}

对于自包含应用程序，然后可以从 
```
  bin/<Debug|Release>/<framework>/<runtime>/publish
```
{: codeblock}
目录推送应用程序。

对于可移植应用程序，可以从 
```
  bin/<Debug|Release>/<framework>/publish
```
{:codeblock}
目录推送应用程序。

另请注意，如果在应用程序中使用 manifest.yml 文件，您可以在 manifest.ymle 中指定发布输出文件夹的路径。之后在推送应用程序时，您无需位于该文件夹中。

## 部署包含多个项目的应用程序
{: #developing_apps_with_multiple_projects}

要部署包含多个项目的应用程序，您需要指定希望 buildpack 将哪个项目作为主要项目运行。在解决方案的根文件夹中创建 .deployment 文件来设置主要项目的路径即可完成此操作。您可以将主要项目的路径指定为项目文件夹或项目文件（.xproj 或 .csproj）。

例如，如果解决方案的 *src* 文件夹中包含 *MyApp.DAL*、*MyApp.Services* 和 *MyApp.Web* 这三个项目，其中 *MyApp.Web* 是主要项目，那么 .deployment 文件的格式应如下所示：
```
  [config]
  project = src/MyApp.Web/MyApp.Web.csproj
```
{: codeblock}

在此示例中，如果在 project.json 文件中将 *MyApp.DAL* 和 *MyApp.Services* 项目列为 *MyApp.Web* 的依赖项，那么 buildpack 会自动编译这两个项目，但 buildpack 只会尝试使用 dotnet run -p src/MyApp.Web 执行主要项目 *MyApp.Web*。
