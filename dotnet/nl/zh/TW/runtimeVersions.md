---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 運行環境版本
{: #runtime_vertsions}


{: shortdesc}

## 支援的版本
{: #supported_versions}
此建置套件支援下列版本，未來的建置套件版本將移除標示為已淘汰的版本。請參閱 [Microsoft 的 LTS 及現行版本的支援聲明](https://www.microsoft.com/net/core/support)。

### project.json 工具（已淘汰）

| .NET SDK 版本| 預設值|
|-------------------------|---------|
| 1.0.0-preview2-003156|   否|

### MSBuild SDK 工具

| .NET SDK 版本| 預設值|
|-------------------------|---------|
| 1.0.3|   否|
| 1.0.4|   是|
| 1.1.0-preview1-005051   |   否|
| 2.0.0-preview1-005977   |   否|
| 2.0.0-preview2-006497   |   否|

### .NET Core 運行環境版本

| .NET Core 運行環境版本| 版本類型| 預設值|
|---------------------------|---------------|---------|
| 1.0.3（已淘汰）| LTS|   否|
| 1.0.4（已淘汰）| LTS|   否|
| 1.0.5                     | LTS|   是|
| 1.1.0（已淘汰）| 現行|   否|
| 1.1.1（已淘汰）| 現行|   否|
| 1.1.2                     | 現行|   否|
| 2.0.0-preview1-002111-00  | LTS（預覽）|   否|
| 2.0.0-preview2-25407-01   | LTS（預覽）|   否|

## 指定 .NET SDK 版本

以應用程式根目錄中選用性的 global.json 來控制 .NET SDK 版本。例如：
```
   {
      "sdk": {
        "version": "2.0.0-preview2-006497"
      }
   }
```
{: codeblock}

如果未指定，則會使用最新「長期支援 (LTS)」GA 運行環境的 MSBuild 工具。若要使用 project.json 工具，您可以指定上面所列的其中一個 project.json 版本，但也應該記住，未來會移除這些版本。
