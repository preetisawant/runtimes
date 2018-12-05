---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 運行環境版本
{: #runtime_versions}

## 支援的版本
{: #supported_versions}

此建置套件支援下列版本，未來的建置套件版本將移除標示為已淘汰的版本。請參閱 [Microsoft 的 LTS 及現行版本的支援聲明](https://www.microsoft.com/net/core/support)。

### project.json 工具（已淘汰）

|.NET SDK 版本|預設值|
|-------------------------|---------|
|1.0.0-preview2-003156|否|

### MSBuild SDK 工具

|.NET SDK 版本|預設值|
|-------------------------|------------------|
| 2.1.301                 |是|
| 2.1.300                 |否|
| 2.1.201                 |否|
| 2.0.3                   |否|
| 2.0.2                   |否|
| 1.1.9                   |否|
|1.0.4|否|


### .NET Core 運行環境版本

|.NET Core 運行環境版本|版本類型|
|---------------------------|-------------------|
| 2.1.1                     |LTS|
| 2.1.0                     |LTS|
| 2.0.7                     |LTS|
| 2.0.3                     |現行|
| 2.0.2                     |現行|
| 2.0.0                     |LTS|
| 1.1.8                     |LTS|
|1.1.2                     |LTS|
| 1.0.11                    |LTS|
|1.0.5                     |LTS|
|1.0.4|LTS|

## 指定 .NET SDK 版本

以應用程式根目錄中選用的 `global.json` 來控制 .NET SDK 版本。例如：
```
   {
      "sdk": {
        "version": "2.1.301"
      }
   }
```
{: codeblock}

如果未指定，則會使用最新的 MSBuild 工具。若要使用 project.json 工具，您可以指定所列的其中一個 project.json 版本，但請記住，未來將會移除這些版本。如果建置套件中未包括指定的版本，則會使用預設版本，並在暫置日誌中出現警告。
