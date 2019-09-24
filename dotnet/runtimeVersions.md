---

copyright:
  years: 2015, 2019
lastupdated: "2019-09-20"
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
| 3.0.100-preview7-012821 |   No             |
| 2.2.401                 |   Yes            |
| 2.2.301                 |   No             |
| 2.2.205                 |   No             |
| 2.1.801                 |   No             |
| 2.1.701                 |   No             |
| 2.1.605                 |   No             |
| 2.1.508                 |   No             |
| 2.1.403                 |   No             |


### .NET Core runtime versions

| .NET Core runtime version | Release type      |
|---------------------------|-------------------|
| 3.0.0-preview7-27912-14   | Normal            |
| 2.2.6                     | Current           |  
| 2.1.12                    | Normal            |
| 2.1.11                    | Normal            |
| 2.1.5                     | Normal            |


### .NET aspnetcore versions

| .NET aspnetcore version | Release type        |
|---------------------------|-------------------|
| 3.0.0-preview7.19365.7    | Normal            |
| 2.2.6                     | Current           |  
| 2.2.5                     | Normal            |
| 2.1.12                    | Normal            |
| 2.1.11                    | Normal            |
| 2.1.5                     | Normal            |




## Specifying the .NET SDK version

Control the .NET SDK version with an optional `global.json` file in the application's root directory. For example:
```
   {
      "sdk": {
        "version": "2.2.401"
      }
   }
```
{: codeblock}

If not specified, the latest MSBuild tooling is used.  To use project.json tooling, you can specify one of the listed project.json versions, but keep in mind that these versions will be removed in the future.  If the specified version is not included in the buildpack, the default version is used, and a warning appears in staging logs.
