---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-12"
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
| 2.1.403                 |   Yes            |
| 2.1.302                 |   No             |
| 2.0.3                   |   No             |
| 1.1.11                  |   No             |
| 1.1.10                  |   No             |
| 1.0.4                   |   No             |


### .NET Core runtime versions

| .NET Core runtime version | Release type      |
|---------------------------|-------------------|
| 2.1.5                     | Current           |  
| 2.1.4                     | LTS               |
| 2.1.2                     | LTS               |
| 2.0.9                     | LTS               |
| 2.0.7                     | LTS               |
| 1.1.10                    | LTS               |
| 1.1.9                     | LTS               |
| 1.0.12                    | LTS               |
| 1.0.11                    | LTS               |


### .NET aspnetcore versions

| .NET aspnetcore version | Release type      |
|---------------------------|-------------------|
| 2.1.5                     | Current           |  
| 2.1.4                     | LTS               |
| 2.1.2                     | LTS               |



## Specifying the .NET SDK version

Control the .NET SDK version with an optional `global.json` file in the application's root directory. For example:
```
   {
      "sdk": {
        "version": "2.1.301"
      }
   }
```
{: codeblock}

If not specified, the latest MSBuild tooling is used.  To use project.json tooling, you can specify one of the listed project.json versions, but keep in mind that these versions will be removed in the future.  If the specified version is not included in the buildpack, the default version is used, and a warning appears in staging logs.
