---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Getting started tutorial
{: #getting-started}

* {: download} Congratulations, you deployed a Hello World sample application on {{site.data.keyword.Bluemix}}!  To get started, follow this step-by-step guide. Or, <a class="xref" href="http://bluemix.net" target="_blank" title="(Download sample code)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Download application code" />download the sample code</a> and explore on your own.

By following the Liberty for Java getting started tutorial, you'll set up a development environment, deploy an app locally and on {{site.data.keyword.Bluemix}}, and integrate a database service in your app.

Throughout these docs, references to the Cloud Foundry CLI are now updated to the {{site.data.keyword.Bluemix_notm}} CLI! The {{site.data.keyword.Bluemix_notm}} CLI has the same familiar Cloud Foundry commands, but with better integration with {{site.data.keyword.Bluemix_notm}} accounts and other services. Learn more about getting started with the {{site.data.keyword.Bluemix_notm}} CLI in this tutorial.
{: tip}

## Before you begin
{: #prereqs}

You'll need the following accounts and tools:
* [{{site.data.keyword.Bluemix_notm}} account](https://cloud.ibm.com/registration)
* [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/ibmcloud/download_cli.html)
* [Git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){: new_window}
* [Maven ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://maven.apache.org/download.cgi){: new_window}

## Step 1: Clone the sample app
{: #clone}

First, clone the sample app GitHub repo.

  ```
git clone https://github.com/IBM-Cloud/get-started-java
  ```
  {: codeblock}


## Step 2: Run the app locally using command line
{: #run_locally}

Use Maven to build your source code and run the resulting app.

1. On the command line, change the directory to where the sample app is located.

  ```
cd get-started-java
  ```
  {: codeblock}

1. Use Maven to install dependencies and build the .war file.

  ```
mvn clean install
  ```
  {: codeblock}

1. Run the app locally on Liberty.

  ```
mvn install liberty:run-server
  ```
  {: codeblock}

When you see the message *The server defaultServer is ready to run a smarter planet.*, you can view your app at: http://localhost:9080/GetStartedJava.

To stop your app, press **Ctrl-C** in the command-line window where you started the app.

## Step 3: Prepare the app for deployment
{: #prepare}

To deploy to {{site.data.keyword.Bluemix_notm}}, it can be helpful to set up a manifest.yml file. The manifest.yml includes basic information about your app, such as the name, how much memory to allocate for each instance and the route. We've provided a sample manifest.yml file in the `get-started-java` directory.

Open the manifest.yml file, and change the `name` from `GetStartedJava` to your app name, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

In this manifest.yml file, **random-route: true** generates a random route for your app to prevent your route from colliding with others.  If you choose to, you can replace **random-route: true** with **host: myChosenHostName**, supplying a host name of your choice.
{: tip}

## Step 4: Deploy to {{site.data.keyword.Bluemix_notm}}
{: #deploy}

You can use the {{site.data.keyword.Bluemix_notm}} CLI to deploy apps.

1. Log in to your {{site.data.keyword.Bluemix_notm}} account, and select an API endpoint.

  ```
ibmcloud login
  ```
  {: codeblock}

  If you have a federated user ID, instead use the following command to log in with your single sign-on ID. See [Logging in with a federated ID](/docs/cli/login_federated_id.html) to learn more.

  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Target a Cloud Foundry org and space:

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  If you don't have an org or a space set up, see [Adding orgs and spaces](/docs/account/orgs_spaces.html).
  {: tip}

1. From within the `get-started-java` directory, push your application to {{site.data.keyword.Bluemix_notm}}.

  ```
ibmcloud cf push
  ```
  {: codeblock}

Deploying your application can take a few minutes. When deployment completes, a message shows that your app is running. View your app at the URL listed in the output of the push command with "/GetStartedJava" appended to the end, or view both the app deployment status and the URL by running the following command:

  ```
ibmcloud cf apps
  ```
  {: codeblock}

You can also go to the {{site.data.keyword.Bluemix_notm}} [Resource List](https://cloud.ibm.com/resources) to view your app. If you click **Visit App URL**, remember to append "/GetStartedJava" to the URL.

You can troubleshoot errors in the deployment process by using the `ibmcloud cf logs GetStartedJava --recent` command.
{: tip}  

## Step 5: Add a database
{: #add_database}

Next, we'll add an {{site.data.keyword.cloudant_short_notm}} NoSQL database to this application and set up the application so that it can run locally and on {{site.data.keyword.Bluemix_notm}}.

1. In your browser, log in to {{site.data.keyword.Bluemix_notm}} and go to the Dashboard. Select **Create resource**.
1. Search for **{{site.data.keyword.cloudant_short_notm}}**, and select the service.
1. For **Available authentication methods**, select **Use both legacy credentials and IAM**. You can leave the default settings for the other fields. Click **Create** to create the service.
1. In the navigation, go to **Connections**, then click **Create connection**. Select your application, and click **Connect**.
1. Using the default values, click **Connect & restage app** to connect the database to your application. Click **Restage** when prompted.

   {{site.data.keyword.Bluemix_notm}} will restart your application and provide the database credentials to your application using the `VCAP_SERVICES` environment variable. This environment variable is available to the application only when it is running on {{site.data.keyword.Bluemix_notm}}.

Environment variables enable you to separate deployment settings from your source code. For example, instead of hardcoding a database password, you can store it in an environment variable that you reference in your source code.
{: tip}

## Step 6: Use the database
{: #use_database}
We're now going to update your local code to point to this database. We'll store the credentials for the services in a properties file. This file will get used ONLY when the application is running locally. When running in {{site.data.keyword.Bluemix_notm}}, the credentials will be read from the `VCAP_SERVICES` environment variable.

1. Find your app in the {{site.data.keyword.Bluemix_notm}} [Resource List](https://cloud.ibm.com/resources). On the Service Details page for your app, click **Connections** in the sidebar. Click the {{site.data.keyword.cloudant_short_notm}} menu icon (**&hellip;**) and select **View credentials**.

2. Copy and paste just the `url` from the credentials to the `url` field of the `src/main/resources/cloudant.properties` file, and save the changes.

  ```
cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:codeblock}

3. Restart the server.

Refresh your browser view at http://localhost:9080/GetStartedJava/. Any names that you enter into the app will now get added to the database.

Your local app and the {{site.data.keyword.Bluemix_notm}} app are sharing the database. Names you add from either app will appear in both when you refresh the browsers.

Remember, if you don't need your app live on {{site.data.keyword.Bluemix_notm}}, stop the app so you don't incur any unexpected charges.
{: tip}  

## Next Steps

* [Tutorials](/docs/tutorials/index.html)
* [Samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
