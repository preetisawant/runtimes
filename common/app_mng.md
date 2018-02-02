---

copyright:
  years: 2015, 2018
lastupdated: "2018-1-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Managing Liberty and Node.js apps
{: #app_management}


App Management is a set of development and debugging utilities that can be enabled for your Liberty and Node.js applications on {{site.data.keyword.Bluemix}}.
{:shortdesc}

## App Management utilities
{: #Utilities}


### Utilities for both Liberty and Node.js
* [proxy](#proxy)
* [noproxy](#noproxy)
* [devconsole](#devconsole)
* [hc](#hc)
* [shell](#shell)

### Liberty utilities
* [debug](#debug)
* [jmx](#jmx)
* [localjmx](#localjmx)

### Node.js utilities
* [inspector](#inspector)
* [trace](#trace)

## How to configure App Management
{: #configure}
To enable App Management utilities, set the value of the *BLUEMIX_APP_MGMT_ENABLE* environment variable to the utility or list of utilities you want to enable, then restage your application. You can enable multiple utilities by separating them with a **+**.

For example, to enable *hc*, *debug* and *trace* utilities, run the following command:

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE hc+debug+trace
```
{: codeblock}

Restage your application after you set the environment variable:

```
cf restage myApp
```
{: codeblock}

If you do not want the App Management utilities to be installed with your application, set the *BLUEMIX_APP_MGMT_INSTALL* environment variable to 'false' and restage your application.

For example, run the following commands to stage your application without App Management utilities:

```
cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
cf restage myApp
```
{: codeblock}

## Restrictions
{: #restrictions}
* Changes that you make to your application by using App Management are transient and are lost after you exit this mode. This mode is only for temporary development use and is not intended to be used as a production environment due to performance.
* For Node.js applications, most App Management utilities do not work if you set your **start** command in the `manifest.yml` file (command) or `CF CLI (-c)`. Those methods are buildpack overrides and are anti-patterns for starting Node.js applications. For best results, set the **start** command in the `package.json` file or `Procfile`.

### Liberty and Node.js utilities
{: #liberty_and_node_utilities}

#### proxy
{: #proxy}

The *proxy* utility provides minimal application management between your application and {{site.data.keyword.Bluemix_notm}}.

When enabled, the buildpack starts a proxy agent that is located between your application's runtime and container.  The *proxy* utility handles all requests that the application receives. Based on the type of request, it either takes an App Management action or forwards the request to your application. By using *proxy*, your application container continues to live even if the application crashes. The proxy agent also allows for incremental file updates, which enables the *Live Edit* mode for Node.js applications.

Some App Management utilities require you to use the *proxy* utility with your application, and can start *proxy* automatically.

#### noproxy
{: #noproxy}

The *noproxy* utility disables the *proxy* utility when it is automatically started by another utility.  With Diego, the proxy is not necessary because Diego provides the capability to *ssh* directly to your application and set up port forwarding.

The *noproxy* utility only applies to applications that run in a Diego cell.

#### devconsole
{: #devconsole}

Users can restart, stop, or suspend their applications with the (*devconsole*) development console utility. Users can also enable or access the shell and inspector utilities by using *devconsole*.  You can use the following URL to access *devconsole*:s
```
  https://<yourappname>.mybluemix.net/bluemix-debug/manage
```
{: codeblock}

For Node version 6.3.0 or greater, the development console provides a restart button for your application and access to the *shell* utility.  See the *inspector* discussion for more information.

**Important**: The *devconsole* utility starts *proxy*.

#### hc
{: #hc}

The (*hc*) Health Center agent enables your application to be monitored by the Health Center client.  For Node.js, the *hc* agent is only available with the Node.js runtime versions included with the IBM SDK for Node.js buildpack.  See [Latest updates to the sdk-for-nodejs buildpack](/docs/runtimes/nodejs/updates.html) for the current set of runtimes.

When you have the Health Center agent enabled, you can analyze the performance of your Liberty and Node.js applications by using the IBM Monitoring and Diagnostic Tools. For more information see [How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}.

**Important:** The *hc* utility starts *proxy*.

**Using *hc* with *noproxy* **

The *hc* utility can be used in conjunction with *noproxy*. To use Health Center with *noproxy*, first establish port forwarding using the `cf ssh` command. For example:

```
cf ssh -N -T -L 1883:127.0.0.1:1883 <appName>
```
{: codeblock}

Next, to connect with the Health Center client, use an [MQTT connection ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SS3KLZ/com.ibm.java.diagnostics.healthcenter.doc/topics/connectingtojvm.html){: new_window} and specify the host as `127.0.0.1` and port as `1883`.

#### shell
{: #shell}

The *shell* utility enables a web-based shell.  You can access the *shell* from the *devconsole* utility or with the following URL:

```
  https://<yourappname>.mybluemix.net/bluemix-debug/shell
```
{: codeblock}

After you access the *shell* utility, a terminal window is displayed with shell access into your application. You can do everything that is supported in a regular shell, such as editing files, checking memory usage, or running diagnostic commands.

**Important:** The *shell* utility also starts *proxy*.

Diego provides an interactive shell through the `cf ssh` command, so the *shell* utility is only useful to applications running on a DEA.
{: .tip}


##### Development Mode for Eclipse Tools
{: #devmode}
Development mode is a feature of the [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html) that gives developers the ability to work with their applications while they are running in the cloud. Development Mode in  Eclipse Tools provides a way for you to work on your applications in {{site.data.keyword.cloud_notm}} with a temporary, secure workspace.

Development mode is supported for both Liberty and Node.js applications. With development mode enabled for your Liberty or Node.js application, you can update application files incrementally without having to push your application. You can also establish a debugging session with your application. Development mode for Liberty applications is equivalent to enabling the *debug* and *jmx* App Management utilities. For Node.js applications, it is equivalent to enabling the *inspector* utility.

### Liberty utilities
{: #liberty_utilities}

#### debug
{: #debug}

To use the *debug* utility, you need to install the [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html).

The *debug* utility puts the Liberty application into debug mode and enables clients such as the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} to establish a [remote debugging](https://console.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html#remotedebug) session with the application.

**Important:** The *debug* utility starts *proxy*.

The *debug* utility can be used in conjunction with *noproxy*. To use debug with *noproxy*, first establish port forwarding using the `cf ssh` command.

The following code snippet shows an example of the `cf ssh` command format:

```
cf ssh -N -T -L 7777:127.0.0.1:7777 <appName>
```
{: codeblock}

Next, to connect in Eclipse, use *Remote Java Configuration* and specify the host as `127.0.0.1` and port as `7777`.

#### jmx
{: #jmx}

The *jmx* utility enables the JMX REST Connector to allow a remote JMX client to manage the application by using {{site.data.keyword.Bluemix_notm}} user credentials.

You can monitor multiple instances of an application by using JMX, but it requires a separate JMX connection for each instance. The default is to monitor instance 0. To monitor instance 1, you can use the following code snip:

```
cf ssh -i 1 -N -T -L 5000:127.0.0.1:5001
```
{: codeblock}

For more information on configuring a JMX connector, see [Configuring secure JMX connection to the Liberty profile ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.

**Important**: The *jmx* utility does not start *proxy*.

#### localjmx
{: #localjmx}

The *localjmx* utility enables the [localConnector-1.0 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feature_localConnector-1.0.html){:new_window} Liberty feature. Combined with local port forwarding, *localjmx* acts an alternate way of allowing a remote JMX client to manage the application.


**Before you begin**: *localjmx* requires you to install JConsole.

The *localjmx* utility is only applicable to applications running on a Diego cell. To use *localjmx*, first establish port forwarding using the `cf ssh` command. For example:

```
cf ssh -N -T -L 5000:127.0.0.1:5000 <appName>
```
{: codeblock}

Next, to connect with JConsole, choose **Remote Process**, specify `127.0.0.1:5000`, and use an insecure connection.


### Node.js utilities
{: #node_utilities}

#### inspector
{: #inspector}

The inspector utility can be used to create CPU usage profiles, add breakpoints, and debug code, all while your application runs on {{site.data.keyword.cloud_notm}}.  For Node.js versions before 6.3.0, the inspector enables the Node inspector debugger interface.  For more information about the Node inspector, see the Readme for [node-inspector on GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/node-inspector/node-inspector){: new_window}.  For Node.js versions 6.3.0 and greater, the *inspector* utility uses the [V8 Inspector Integration for Node.js ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://nodejs.org/dist/latest-v6.x/docs/api/debugger.html#debugger_v8_inspector_integration_for_node_js){:new_window}.

##### **For Node.js versions after 6.3.0**
When you start debugging mode, *proxy* is automatically enabled, even if you use a version of Node.js that does not include *proxy*. Versions of Node.js after 6.3.0 do not include *proxy.* If you use the *inspector* utility with versions of Node.js after 6.3.0, you can turn off *proxy* again by using *noproxy.*

Instead of using *proxy* to access the *inspector* interface, you use the Developer Tools capability of the Google Chrome web browser.  

Enable access to the URL with local port forwarding with the following command:
```
cf ssh -N -T -L 9229:127.0.0.1:9229 <appName>
```
{: codeblock}

Get the startup log for the application by using the following command.
```
cf logs <appName> --recent
```
{: codeblock}

If the *inspector* utility is active, the log contains messages similar to the following:
```
 ... You will need a SSH tunnel for port 9229 to be able to use the Chrome DevTools to remotely debug your app
 ... Starting app with 'node --inspect=9229  app.js '
```
{: codeblock}

Use an up-to-date version of the Google Chrome web browser to browse to `chrome://inspect`.
From this URL, you see your app listed along with a link to your applictation files such as `file://home/vcap/app/app.js`., then select **inspect** to access the inspect interface.

##### **For Node.js versions before 6.3.0**
If you use the *proxy,* you can access the *inspector* interface at `https://myApp.mybluemix.net/bluemix-debug/inspector`.

If you do not use the *proxy* utility, enable access to the application URL by using local port forwarding with the following command:

```
cf ssh -N -T -L 8790:127.0.0.1:8790 <appName>
```
{: codeblock}

Then, access the inspector from the URL, `http://127.0.0.1:8790`.

#### trace (deprecated)
{: #trace}

The trace utility allows you to dynamically sets trace levels if your application is using log4js, ibmbluemix, or bunyan logging modules.

Navigate to the **Instance Details** page in the {{site.data.keyword.cloud_notm}} web console and select **Actions** to see the UI.

Note: Supported dependency versions:

* log4js:(0.6.0 - 0.6.24)
* bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
* ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)


The trace utility is not available when the application starts using the `-b buildpack` option.

The trace utility does not start *proxy*.
