---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-20"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 運行環境版本
{: #runtime_versions}

## 支援的版本
{: #supported_versions}

此建置套件支援下列版本，未來的建置套件版本將移除標示為已淘汰的版本。請參閱 [Microsoft 的 LTS 及現行版本的支援聲明](https://www.microsoft.com/net/core/support)。


### .NET SDK 版本

|.NET SDK 版本|預設值|
|-------------------------|------------------|
| 2.2.104                 |是|
| 2.1.504                 |否|
| 2.1.403                 |否|
| 2.0.3                   |否|
| 1.1.12                  |否|
| 1.1.11                  |否|
|1.0.4|否|


### .NET Core 運行環境版本

|.NET Core 運行環境版本|版本類型|
|---------------------------|-------------------|
| 2.2.2                     |現行|  
| 2.2.1                     |LTS|
| 2.1.8                     |LTS|
| 2.1.7                     |LTS|
| 2.0.9                     |LTS|
| 2.0.7                     |LTS|
| 1.1.11                  |LTS|
| 1.1.10                    |LTS|
| 1.0.12                    |LTS|
| 1.0.11                    |LTS|


### .NET aspnetcore 版本

| .NET aspnetcore 版本 |版本類型|
|---------------------------|-------------------|
| 2.2.2                     |現行|  
| 2.2.1                     |LTS|
| 2.1.8                     |LTS|
| 2.1.7                     |LTS|



## 指定 .NET SDK 版本

以應用程式根目錄中選用的 `global.json` 來控制 .NET SDK 版本。例如：
```
   {
      "sdk": {
        "version": "2.2.104"
      }
   }
```
{: codeblock}

如果未指定，則會使用最新的 MSBuild 工具。若要使用 project.json 工具，您可以指定所列的其中一個 project.json 版本，但請記住，未來將會移除這些版本。如果建置套件中未包括指定的版本，則會使用預設版本，並在暫置日誌中出現警告。
