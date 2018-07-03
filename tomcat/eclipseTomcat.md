---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-03"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Develop Tomcat applications using IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}

You can also use {{site.data.keyword.eclipsetoolsfull}} as an alternative way to develop and deploy applications to {{site.data.keyword.Bluemix}}. IBM Eclipse Tools provide plug-ins that can be installed into an existing Eclipse environment to assist in integrating your integrated development environment (IDE) with {{site.data.keyword.Bluemix_notm}}.

This procedure follows the same general steps as the [Getting started tutorial](getting-started.html) for Liberty. Using Eclipse, you'll set up a development environment, deploy an app locally and on the cloud, and integrate a database service in your app.

## Before you begin
{: #prereqs}

You'll need the following accounts and tools:
* [IBM Eclipse Tools for IBM Cloud ![External Link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}
* [Eclipse IDE for Java EE Developers ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}

If you completed the [Getting started tutorial](getting-started.md), you might already have these tools and accounts. Be sure you also have the following installed and registered before you start:
* [{{site.data.keyword.Bluemix_notm}} account](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} CLI](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){: new_window}
* [Maven ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat version 8.0.41 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}

## Step 1: Clone the sample app
{: #clone}

First, clone the sample app GitHub repo.

  ```
git clone https://github.com/IBM-Cloud/get-started-tomcat
  ```
  {: codeblock}

## Step 2: Build your application's source code
{: #build_app}

Use Maven to build your source code and run the resulting app.

1. On the command line, change the directory to where the sample app is located.

  ```
cd get-started-tomcat
  ```
  {: codeblock}

1. Use Maven to install dependencies and build the .war file.

  ```
mvn clean install
  ```
  {: codeblock}

## Step 3: Prepare the app for deployment
{: #prepare}

To deploy to {{site.data.keyword.Bluemix_notm}}, it can be helpful to set up a manifest.yml file. The manifest.yml includes basic information about your app, such as the name, how much memory to allocate for each instance and the route. We've provided a sample manifest.yml file in the `get-started-java` directory.

Open the manifest.yml file, and change the `name` from `GetStartedJava` to your app name, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

```
applications:
- name: GetStartedTomcat
  random-route: true
  memory: 256M
  path: target/GetStartedTomcat.war
  buildpack: java_buildpack
```
{: codeblock}

In this manifest.yml file, **random-route: true** generates a random route for your app to prevent your route from colliding with others.  If you choose to, you can replace **random-route: true** with **host: myChosenHostName**, supplying a host name of your choice.
{: tip}

## Step 4: Log in to {{site.data.keyword.Bluemix_notm}}
{: #deploy}

1. Log in to your {{site.data.keyword.Bluemix_notm}} account, and select an API endpoint.
  ```
ibmcloud login
  ```
  {: codeblock}

  If you cannot log in using `ibmcloud login` because you have a federated user ID, use the following to log in with your single sign on ID. See [Logging in with a federated ID](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) to learn more.
  ```
ibmcloud login --sso
  ```
  {: codeblock}

  Next, target the Cloud Foundry CLI:
  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  If you don't have an org or a space set up, see [Adding orgs and spaces](https://console.bluemix.net/docs/account/orgs_spaces.html).
  {: tip}

## Step 5: Develop using Eclipse
{: #eclipse}

1. Make sure that you have the [IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix).

2. Import the `get-started-java` sample into Eclipse by going to **File > Import > Maven > Existing Maven Projects**.

3. Create a Tomcat server definition:
  - In the **Servers** view, right-click and select **New > Server**.
  - Select **Apache > Tomcat v8.0 Server**.
  - Choose your `tomcat-install-dir`.
  - Continue the wizard with default options to finish.

4. Run your application locally on the Apache server:
  - Right click on the `GetStartedTomcat` sample and select **Run As > Run on Server**.
  - Find and select the localhost Tomcat server, and click **Finish**.
  - In a few seconds, your application will be running at http://localhost:8080/GetStartedTomcat/

5. Run your application on {{site.data.keyword.Bluemix_notm}}:
  - Right-click on the `GetStartedTomcat` sample, and select **Run As > Run on Server**.
  - Find and select **{{site.data.keyword.Bluemix_notm}}**, and then click **Finish**.
  - A wizard will guide you with the deployment options. Be sure to choose a unique `Name` for your application.
  - In a few minutes, your application will be running at the URL you chose.

Now you have run your code both locally and on the cloud!

## Step 6: Add a database
{: #add_database}

Next, we'll add a {{site.data.keyword.cloudantfull}} database to this application and set up the application so that it can run locally and on {{site.data.keyword.Bluemix_notm}}.

1. In your browser, log in to {{site.data.keyword.Bluemix_notm}} and go to the Dashboard. Select **Create Resource**.
2. Choose the **Data and Analytics** section, then select **{{site.data.keyword.cloudant_short_notm}}** and create your service.
3. Go to the  **Connections** view and select your application, then **Create connection**.
4. Select **Restage** when prompted. {{site.data.keyword.Bluemix_notm}} will restart your application and provide the database credentials to your application using the `VCAP_SERVICES` environment variable. This environment variable is available to the application only when it is running on {{site.data.keyword.Bluemix_notm}}.

Environment variables enable you to separate deployment settings from your source code. For example, instead of hardcoding a database password, you can store this in an environment variable which you reference in your source code.
{: tip}

## Step 7: Use the database
{: #use_database}
We're now going to update your local code to point to this database. We'll store the credentials for the services in a properties file. This file will get used ONLY when the application is running locally. When running in {{site.data.keyword.Bluemix_notm}}, the credentials will be read from the VCAP_SERVICES environment variable.

1. Open Eclipse and open the file src/main/resources/cloudant.properties:

  ```
  cloudant_url=
  ```
  {: codeblock}

2. In your browser open the {{site.data.keyword.Bluemix_notm}} UI, select your App -> Connections -> Cloudant -> View Credentials

3. Copy and paste just the `url` from the credentials to the `url` field of the `cloudant.properties` file and save the changes.  The result will be something like:

  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {: codeblock}

4. Restart Tomcat server in Eclipse from the `Servers` view.

  Refresh your browser view at: http://localhost:8080/GetStartedTomcat/. Any names you enter into the app will now get added to the database.

  Your local app and the {{site.data.keyword.Bluemix_notm}} app are sharing the database.  View your {{site.data.keyword.Bluemix_notm}} app at the URL listed in the output of the push command from above.  Names you add from either app should appear in both when you refresh the browsers.

Remember if you don't need your app live on {{site.data.keyword.Bluemix_notm}}, stop it so you don't incur any unexpected charges.
{: tip}
