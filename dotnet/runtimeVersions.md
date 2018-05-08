---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Runtime Versions
{: #runtime_versions}


{: shortdesc}

## Supported versions
{: #supported_versions}

This buildpack supports the following versions, those marked as deprecated will be removed in a future buildpack release.  See [Microsoft's support statement for LTS and Current releases](https://www.microsoft.com/net/core/support).

### project.json tooling (deprecated)

| .NET SDK version        | Default |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   No    |

### MSBuild SDK tooling

| .NET SDK version        | Default          |
|-------------------------|------------------|
| 1.0.4                   |   No             |
| 1.1.0                   |   Yes (F# only)  |
| 2.0.0                   |   Yes            |

### .NET Core runtime versions

| .NET Core runtime version | Release type      |
|---------------------------|-------------------|
| 1.0.4 (deprecated)        | LTS               |
| 1.0.5                     | LTS               |
| 1.1.1 (deprecated)        | LTS               |
| 1.1.2                     | LTS               |
| 2.0.0-preview2-25407-01   | Current (preview) |
| 2.0.0                     | Current           |

## Specifying the .NET SDK version

Control the .NET SDK version with an optional `global.json` file in the application's root directory. For example:
```
   {
      "sdk": {
        "version": "2.0.0"
      }
   }
```
{: codeblock}

If not specified, the latest MSBuild tooling is used.  To use project.json tooling, you can specify one of the listed project.json versions, but keep in mind that these versions will be removed in the future.  If the specified version is not included in the buildpack, the default version is used, and a warning appears in staging logs.
