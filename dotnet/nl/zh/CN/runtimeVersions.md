---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 运行时版本
{: #runtime_vertsions}


{: shortdesc}

## 受支持的版本
{: #supported_versions}
此 buildpack 支持以下版本，那些标记为不推荐的版本将在未来 buildpack 发行版中除去。请参阅 [Microsoft 对 LTS 和当前发行版的支持声明](https://www.microsoft.com/net/core/support)。

### project.json 工具（不推荐）

| .NET SDK 版本   | 缺省   |
|-------------------------|---------|
| 1.0.0-preview2-003156|   否|

### MSBuild SDK 工具

| .NET SDK 版本   | 缺省   |
|-------------------------|---------|
| 1.0.3|   否|
| 1.0.4|   是   |
| 1.1.0-preview1-005051   |   否|
| 2.0.0-preview1-005977   |   否|
| 2.0.0-preview2-006497   |   否|

### .NET 核心运行时版本

| .NET 核心运行时版本      | 发行版类型  | 缺省   |
|---------------------------|---------------|---------|
| 1.0.3（不推荐）        | LTS|   否|
| 1.0.4（不推荐）        | LTS|   否|
| 1.0.5                  | LTS|   是|
| 1.1.0（不推荐）        | 当前   |   否|
| 1.1.1（不推荐）        | 当前   |   否|
| 1.1.2                  | 当前   |   否|
| 2.0.0-preview1-002111-00  | LTS（预览） |   否|
| 2.0.0-preview2-25407-01   | LTS（预览） |   否|

## 指定 .NET SDK 版本

使用应用程序根目录中的可选 global.json 来控制 .NET SDK 版本。例如：
```
   {
      "sdk": {
        "version": "2.0.0-preview2-006497"
      }
   }
```
{: codeblock}

如果未指定，将使用最新的长期支持 (LTS) GA 运行时的 MSBuild 工具。要使用 project.json 工具，可以指定上面列出的其中一个 project.json 版本，但同时应该谨记这些版本未来将会除去。
