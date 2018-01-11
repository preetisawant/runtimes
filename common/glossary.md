---

copyright:
  years: 2017
lastupdated: "2017-11-28"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Glossary of terms

This page provides definitions for a variety of terms associated with {{site.data.keyword.Bluemix}} and Cloud Foundry.
{:shortdesc}

  *  Cloud Foundry

     According to [cloudfoundry.org](https://www.cloudfoundry.org/learn/)
     Cloud Foundry is an open source platform for application lifecycle automation.  {{site.data.keyword.Bluemix}}
     is built on top of the Cloud Foundry platform as a service.

  *  Cloud Foundry Application

     A cloud foundry application or app, is any application intended to be instantiated by on one of the buildpacks provided by
     {{site.data.keyword.Bluemix_notm}}.

  *  Buildpack

     A buildpack is a typically language specific package of software provided by {{site.data.keyword.Bluemix_notm}}. When an application is deployed to {{site.data.keyword.Bluemix_notm}} a buildpack appropriate for the application is chosen. The buildpack provisions the runtime environment for the application.  You can see the set of buildpacks provided by {{site.data.keyword.Bluemix_notm}} by issuing the `cf buildpacks` command from the command line.

  *  Runtime

     A runtime is the sef of software components that provide the exectuion environment for an application.  The terms *runtime* and *buildpack* are sometimes used interchangeably.  When a buildpack has completed deploying an application the runtime environment is established.

  *  Boilerplate

     A boilerplate is a simple application designed for a particular runtime.  The boilerplates provide templates or samples of the language and runtime specific application types.  You can use a boilerplate as starter code to begin development of more sophisticated applications.  {{site.data.keyword.Bluemix_notm}} provides:
     * *Hello world boilerplates* which are very simple applications typically providing a language and runtime specific 'hello world' application.
     * *Boilerplates with services* which demonstrate how to use a runtime with a service.
     * *Boilerplates with frameworks* which are simple language and runtime specific applications that take advantage of a particulary language framework such as Python Flask or Ruby Sinatra.

  *  Service

     A service is a {{site.data.keyword.Bluemix_notm}} provided
     facility which can be coupled with an application.
