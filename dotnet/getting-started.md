---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-30"

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
{: #getting_started}

* {: download} Congratulations, you deployed a Hello World sample application on {{site.data.keyword.Bluemix}}!  To get started, follow this step-by-step guide. Or, <a class="xref" href="http://bluemix.net" target="_blank" title="(Download sample code)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Download application code" />download the sample code</a> and explore on your own.

By following this getting started tutorial, you'll set up a development environment, deploy an app locally and on {{site.data.keyword.Bluemix}}, and integrate an {{site.data.keyword.Bluemix}} database service in your app.

## Before you begin
{: #prereqs}

You'll need the following:
* [{{site.data.keyword.Bluemix_notm}} account](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} CLI](../../cli/reference/ibmcloud/download_cli.html)
* [Git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){: new_window}
* Install .NET Core 2.1.1 SDK 2.1.301 from the [.NET Core downloads website ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.microsoft.com/net/download/core).

## Step 1: Clone the sample app
{: #clone}

First, clone the sample app GitHub repo.
  ```
git clone https://github.com/IBM-Cloud/get-started-aspnet-core
  ```
  {: codeblock}


## Step 2: Run the app locally
{: #run_locally}

1. On the command line, change the directory to where the sample app is located.

  ```
  cd get-started-aspnet-core/src/GetStartedDotnet
  ```
  {: codeblock}

1. Run the app locally by running the following commands.

  ```
dotnet restore
  ```
  {: codeblock}

  ```
dotnet run
  ```
  {: codeblock}

1. View your app at: http://localhost:5000/.

## Step 3: Prepare the app for deployment
{: #prepare}

To deploy to {{site.data.keyword.Bluemix_notm}}, it can be helpful to set up a manifest.yml file. The manifest.yml includes basic information about your app, such as the name, how much memory to allocate for each instance and the route. We've provided a sample manifest.yml file in the `get-started-dotnet` directory.

Open the manifest.yml file, and change the `name` from `GetStartedDotnet` to your app name, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedDotnet
   random-route: true
   memory: 512M
  ```
  {: codeblock}

In this manifest.yml file, **`random-route: true`** generates a random route for your app to prevent your route from colliding with others.  If you choose to, you can replace **`random-route: true`** with **`host: myChosenHostName`**, supplying a host name of your choice.
{: tip}

## Step 4: Deploy the app
{: #deploy}

You can use the {{site.data.keyword.Bluemix_notm}} CLI to deploy apps.

1. Log in to your {{site.data.keyword.Bluemix_notm}} account, and select an API endpoint.
  ```
ibmcloud login
  ```
  {: codeblock}

  If you have a federated user ID, instead use the following command to log in with your single sign-on ID. See [Logging in with a federated ID](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) to learn more.
 ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Target a Cloud Foundry org and space:
  ```
ibmcloud target --cf
  ```
  {: codeblock}

  If you don't have an org or a space set up, see [Adding orgs and spaces](https://console.bluemix.net/docs/account/orgs_spaces.html).
  {: tip}

1. **Be sure you are in the main directory, `get-started-aspnet-core`, for your application**  then push your application to {{site.data.keyword.Bluemix_notm}}:
  ```
ibmcloud cf push
  ```
  {: codeblock}

  This can take a minute. If there is an error in the deployment process, you can use the command `ibmcloud cf logs <Your-App-Name> --recent` to troubleshoot.

When deployment completes, you should see a message indicating that your app is running.  View your app at the URL listed in the output of the push command.  You can also issue the following command to view your app's status and to see the URL.
  ```
ibmcloud cf apps
  ```
  {: codeblock}

## Step 5: Add a database
{: #add_database}

Next, we'll add an {{site.data.keyword.cloudant_short_notm}} NoSQL database to this application and set up the application so that it can run locally and on {{site.data.keyword.Bluemix_notm}}.

1. In your browser, log in to {{site.data.keyword.Bluemix_notm}} and go to the Dashboard. Select **Create resource**.
1. Search for **{{site.data.keyword.cloudant_short_notm}}**, and select the service.
1. For **Available authentication methods**, select **Use both legacy credentials and IAM**. You can leave the default settings for the other fields. Click **Create** to create the service.
1. In the navigation, go to **Connections**. Select your application, and click **Create connection**.
1. Connect to your application using the default values, and click **Connect & restage app**. Then, click **Restage** when prompted.

   {{site.data.keyword.Bluemix_notm}} will restart your application and provide the database credentials to your application using the `VCAP_SERVICES` environment variable. This environment variable is available to the application only when it is running on {{site.data.keyword.Bluemix_notm}}.

Environment variables enable you to separate deployment settings from your source code. For example, instead of hardcoding a database password, you can store it in an environment variable that you reference in your source code.
{: tip}

## Step 6: Use the database locally
{: #use_database}

We're now going to update your local code to point to this database. We'll store the credentials for the services in a JSON file. This file will get used ONLY when the application is running locally. When running in {{site.data.keyword.Bluemix_notm}}, the credentials will be read from the `VCAP_SERVICES` environment variable.

1. In the `src/GetStartedDotnet` directory, create a `vcap-local.json` file.

1. Copy and paste the following JSON object into the `vcap-local.json` file, and save your changes.

   ```json
   {
     "services": {
       "cloudantNoSQLDB": [
         {
           "credentials": {
             "url":"CLOUDANT_DATABASE_URL"
           },
           "label": "cloudantNoSQLDB"
         }
       ]
     }
   }
   ```
   {: codeblock}

1. In your browser, go to the {{site.data.keyword.Bluemix_notm}} dashboard and select **_your app_ > Connections**. Click the {{site.data.keyword.cloudant_short_notm}} menu icon (**&vellip;**) and select **View credentials**.

1. Copy and paste just the `url` value from the credentials to the `url` field of the `vcap-local.json` file, replacing `CLOUDANT_DATABASE_URL`.

1. From the `get-started-aspnet-core/src/GetStartedDotnet` directory, restart your application by running the following command.

   ```
   dotnet run
   ```
   {: codeblock}

1. Refresh your browser view at http://localhost:5000/. Any names you enter into the app will now get added to the database.

Your local app and the {{site.data.keyword.Bluemix_notm}} app share the database.  View your {{site.data.keyword.Bluemix_notm}} app at the URL listed in the output of the `ibmcloud cf push` command.  Names you add from either app should appear in both when you refresh the browsers.

Remember, if you don't need your app live, stop it so you don't incur any unexpected charges.
{: tip}

## Next Steps

* [Tutorials](/docs/tutorials/index.html)
* [Samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
