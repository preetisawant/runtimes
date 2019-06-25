---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-21"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Runtime Versions
{: #runtime_versions}

## Supported versions
{: #supported_versions}

This buildpack supports the following versions, those marked as deprecated will be removed in a future buildpack release.  See [Microsoft's support statement for LTS and Current releases](https://www.microsoft.com/net/core/support).


### .NET SDK version

| .NET SDK version        | Default          |
|-------------------------|------------------|
| 2.2.204                 |   Yes            |
| 2.2.203                 |   No             |
| 2.2.107                 |   No             |
| 2.1.507                 |   No             |
| 2.1.403                 |   No             |
| 1.1.14                  |   No             |
| 1.1.13                  |   No             |


### .NET Core runtime versions

| .NET Core runtime version | Release type      |
|---------------------------|-------------------|
| 2.2.5                     | Current           |  
| 2.2.4                     | Normal            |
| 2.1.11                    | Normal            |
| 2.1.10                    | Normal            |
| 2.1.5                     | Normal            |
| 1.1.13                    | Normal            |
| 1.1.12                    | Normal            |


### .NET aspnetcore versions

| .NET aspnetcore version | Release type        |
|---------------------------|-------------------|
| 2.2.5                     | Current           |  
| 2.2.4                     | Normal            |
| 2.1.11                    | Normal            |
| 2.1.10                    | Normal            |
| 2.1.5                     | Normal            |




## Specifying the .NET SDK version

Control the .NET SDK version with an optional `global.json` file in the application's root directory. For example:
```
   {
      "sdk": {
        "version": "2.2.204"
      }
   }
```
{: codeblock}

If not specified, the latest MSBuild tooling is used.  To use project.json tooling, you can specify one of the listed project.json versions, but keep in mind that these versions will be removed in the future.  If the specified version is not included in the buildpack, the default version is used, and a warning appears in staging logs.
