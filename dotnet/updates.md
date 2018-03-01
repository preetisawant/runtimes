---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-06"
---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Latest Updates to the ASP.NET Core buildpack
{: #latest_updates}


A list of the latest updates in the aspnet buildpack.

## October 6, 2017: Updated ASP.NET Core buildpack v1.0.26-20170913-1346
* Add support for .NET Core runtime 2.0.0
* Add support for .NET Core SDK 1.1.0
* Add support for .NET Core SDK 2.0.0
* Remove support for .NET Core SDK 1.1.0-preview1-005051
* Remove support for .NET Core SDK 2.0.0-preview1-005977
* Remove support for .NET Core runtime 1.0.3
* Remove support for .NET Core runtime 1.1.0
* Update Node version to 6.11.2
* Change default .NET Core SDK to 2.0.0
* Change default .NET Core SDK for F# projects to 1.1.0

## July 24, 2017: Updated ASP.NET Core buildpack v1.0.22-20170724-0813

* Add support for .NET Core runtime 2.0.0 Preview 2
* Add support for .NET Core SDK 1.1.0-preview1-005051
* Add support for .NET Core SDK 2.0.0-preview2-006497
* Update Node version to 6.11.1
* Always make self-contained applications executable

## June 20, 2017: Updated ASP.NET Core buildpack v1.0.20-20170620-1449

* Add support for .NET Core runtime 2.0.0 Preview 1
* Add support for .NET Core SDK 2.0.0-preview1-005977
* Update Node version to 6.10.3
* Remove support for .NET Core runtime version 1.0.0
* Remove support for .NET Core runtime version 1.0.1
* Remove support for .NET Core SDK version 1.0.0-preview2-1-003177
* Add staging_task.log file to application container
* Lower disk usage when caching dependencies

## May 12, 2017: Updated ASP.NET Core buildpack v1.0.18-20170516-1601

* Add support for .NET Core runtime 1.0.5
* Add support for .NET Core runtime 1.1.2
* Add support for .NET Core SDK 1.0.3
* Add support for .NET Core SDK 1.0.4
* Update Node version to 6.10.2
* Remove support for .NET Core SDK 1.0.1
* Remove support for .NET Core SDK 1.0.0-preview4-004233
* Use ASPNETCORE_URLS environment variable to specify port

## Mar 29, 2017: Updated ASP.NET Core buildpack v1.0.13-20170330-1023

* Add support for .NET Core runtime 1.0.4
* Add support for .NET Core runtime 1.1.1
* Add support for .NET Core SDK 1.0.1
* Update Node version to 6.10.0
* Remove support for .NET Core SDK 1.0.0-preview2-003131
* Remove support for .NET Core SDK 1.0.0-preview3-004056

## Jan 31, 2017: Updated ASP.NET Core buildpack v1.0.10-20170124-1145

* Add support for .NET Core 1.0.3
* Add support for .NET Core MSBuild tooling
* Add support for F# projects
* Remove support for .NET Core SDK 1.0.0-preview2-003121

## Dec 9, 2016: Updated ASP.NET Core buildpack v1.0.6-20161205-0912

* Add support for .NET Core 1.1.0
* Remove support for .NET Core 1.0.0 RC2
* Add an option to clear NuGet packages cache

## Oct 10, 2016: Updated ASP.NET Core buildpack v1.0.1-20161005-1225

* Add support for .NET Core 1.0.1
* Fix an intermittent issue which caused deployment to fail when caching NuGet packages

## Aug 31, 2016: Updated ASP.NET Core buildpack v1.0-20160826-1345

* Add support for running pre and post compile scripts using NPM and Bower to install front-end javascript and css libraries.
* Move buildpack from Beta status to GA status

## July 11, 2016: Updated ASP.NET Core buildpack v0.9-20160706-1603

This version of the buildpack includes the following changes:

* This version of the buildpack supports the .NET CLI 1.0 Preview 2 build and .NET Core 1.0 RTM
* The buildpack continues to support .NET CLI 1.0 Preview 1 and .NET Core 1.0 RC2
* The default .NET CLI version to be installed is now 1.0.0-preview2-003121

## June 10, 2016: Updated ASP.NET Core buildpack v0.8.1-20160526-0957

This version of the buildpack includes the following changes:

* The runtime's name is changed from ASP.NET 5 to ASP.NET Core.
* The buildpack version number is included in detect script output.
* This version of the buildpack removes support for DNX based applications using CoreCLR RC1 and lower.
* This version of the buildpack supports the .NET CLI and .NET Core RC2.
* The buildpack detects projects with either a project.json file or *.runtimeconfig.json files from publish output.

## October 22, 2015: Updated ASP.NET 5 buildpack v0.7-20151022-1257

* This version of the buildpack removes Mono and instead supports the Beta 8 CoreCLR.

## September 18, 2015: Updated ASP.NET 5 buildpack v0.6-20150916-1220

* This version of the buildpack supports Beta 7 DNX changes, and it can run applications dependent on older beta releases with the following custom start command:

```
   dnx src/dotnetstarter kestrel --server.urls http://${VCAP_APP_HOST}:${PORT}
```
{: codeblock}

* Usage of the Nowin web server was removed from this buildpack and the [Kestrel]{https://github.com/aspnet/KestrelHttpServer} web server is used instead.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Dotnet core runtime](index.html)
