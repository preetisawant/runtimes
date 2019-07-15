---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 运行时版本
{: #runtime_versions}


{: shortdesc}

## 受支持的版本
{: #supported_versions}

此 buildpack 支持以下版本，那些标记为不推荐的版本将在未来 buildpack 发行版中除去。请参阅 [Microsoft 对 LTS 和当前发行版的支持声明](https://www.microsoft.com/net/core/support)。

### project.json 工具（不推荐）

|.NET SDK 版本   |缺省   |
|-------------------------|---------|
|1.0.0-preview2-003156|否|

### MSBuild SDK 工具

|.NET SDK 版本   |缺省   |
|-------------------------|------------------|
| 1.0.4                   |   否             |
| 1.1.0                   |   是（仅限 F#）  |
| 2.0.0                   |   是             |

### .NET 核心运行时版本

|.NET 核心运行时版本      |发行版类型  |
|---------------------------|-------------------|
|1.0.4（不推荐）        |LTS|
|1.0.5                  |LTS|
|1.1.1（不推荐）        |LTS|
|1.1.2                  |LTS|
|2.0.0-preview2-25407-01   |当前（预览）|
|2.0.0                     |当前        |

## 指定 .NET SDK 版本

可以使用应用程序根目录中的可选 `global.json` 文件来控制 .NET SDK 版本。例如：
```
   {
      "sdk": {
        "version": "2.0.0"
      }
   }
```
{: codeblock}

如果未指定，将使用最新的 MSBuild 工具。要使用 project.json 工具，可以指定上面列出的其中一个 project.json 版本，但请注意，这些版本将来会被除去。如果指定的版本未包含在 buildpack 中，那么将使用缺省版本，并会在编译打包日志中显示一条警告。
