---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

Liberty for Java applications on {{site.data.keyword.Bluemix}} are powered by the liberty-for-java buildpack. The liberty-for-java buildpack provides a complete runtime environment for running Java EE 7 and OSGi applications on top of WebSphere Liberty. It supports popular frameworks like Spring and includes the {{site.data.keyword.IBM_notm}} JRE. Liberty enables rapid application development that is well suited to the cloud.
{: shortdesc}

## Detection
{: #detection}
The Liberty buildpack is used when the following kinds of applications are deployed:
* [WAR files](optionsForPushing.html#stand_alone_apps)
* [EAR files](optionsForPushing.html#stand_alone_apps)
* [Liberty server directory](optionsForPushing.html#server_directory)
* [Liberty packaged server](optionsForPushing.html#packaged_server)
* Java main
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## Starter application
{: #starter_application}
{{site.data.keyword.Bluemix_notm}} provides several Liberty starter applications.  The Liberty starter applications are simple Liberty apps that provide a template that you can use. You can experiment with the starter apps, and make and push changes to the {{site.data.keyword.Bluemix_notm}} environment.  See [Using the starter applications](../common/starter_app_usage.html) for help with using the starter applications.
