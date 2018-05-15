---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-10"

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

By following the Dotnet getting started tutorial you'll set up a development environment, deploy an app locally and on {{site.data.keyword.Bluemix}}, and integrate a {{site.data.keyword.Bluemix}} database service in your app.

## Before you begin
{: #prereqs}

You'll need the following:
* [{{site.data.keyword.Bluemix_notm}} account](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){: new_window}
* Install .NET Core 1.1 SDK 1.0.4 from the [dot.net website ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.microsoft.com/net/download/core) instructions.

## Step 1: Clone the sample app
{: #clone}

Now you're ready to start working with the app. Clone the repository and change to the directory where the sample app is located.
  ```
git clone https://github.com/IBM-Cloud/get-started-aspnet-core
  ```
  {: pre}
  ```
cd get-started-aspnet-core
  ```
  {: pre}

## Step 2: Run the app locally
{: #run_locally}

Run the app.
  ```
cd src/GetStartedDotnet
  ```
  {: pre}
  ```
dotnet restore
  ```
  {: pre}
  ```
dotnet run
  ```
  {: pre}

View your app at: http://localhost:5000/

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

In this manifest.yml file, **random-route: true** generates a random route for your app to prevent your route from colliding with others.  If you choose to, you can replace **random-route: true** with **host: myChosenHostName**, supplying a host name of your choice. [Learn more...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## Step 4: Deploy the app
{: #deploy}

You can use the Cloud Foundry CLI to deploy apps.

To start, login to your {{site.data.keyword.Bluemix_notm}} account:
  ```
cf login
  ```
  {: pre}

  If you cannot log in using the `cf login` or `bx login` commands because you have a federated user ID, use either the `cf login --sso` or   `bx login --sso` commands to log in with your single sign on ID. See [Logging in with a federated ID](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) to learn more.

Choose your API endpoint
  ```
cf api <API-endpoint>
  ```
  {: pre}

Replace the *API-endpoint* in the command with an API endpoint from the following list.

| **Region name** | **Geographic location** | **API endpoint** |
|-----------------|-------------------------|-------------------|
| US South region | Dallas, US | api.ng.bluemix.net |
| US East region | Washington, DC, US | api.us-east.bluemix.net |
| United Kingdom region | London, England | api.eu-gb.bluemix.net |
| Sydney region | Sydney, Australia | api.au-syd.bluemix.net |
| Germany region | Frankfurt, Germany | api.eu-de.bluemix.net |
{: caption="Table 1. {{site.data.keyword.cloud_notm}} region list" caption-side="top"}

**Be sure you are in the main directory, `get-started-aspnet-core`, for your application**  them push your application to {{site.data.keyword.Bluemix_notm}}
  ```
cf push
  ```
  {: pre}

This can take a minute. If there is an error in the deployment process you can use the command `cf logs <Your-App-Name> --recent` to troubleshoot.

When deployment completes you should see a message indicating that your app is running.  View your app at the URL listed in the output of the push command.  You can also issue the
  ```
cf apps
  ```
  {: pre}
  command to view your apps status and see the URL.

## Step 5: Connect a MySQL database
{: connect_mysql}

Next, we'll add a ClearDB MySQL database to this application and set up the application so that it can run locally and on {{site.data.keyword.Bluemix_notm}}.

1. In your browser, log in to {{site.data.keyword.Bluemix_notm}} and go to the Dashboard. Select **Create Resource**.
2. Choose the **Data and Analytics** section, then select **ClearDB MySQL** and create your service.
3. Go to the  **Connections** view and select your application, then **Create connection**.
4. Select **Restage** when prompted. {{site.data.keyword.Bluemix_notm}} will restart your application and provide the database credentials to your application using the `VCAP_SERVICES` environment variable. This environment variable is available to the application only when it is running on {{site.data.keyword.Bluemix_notm}}.

Environment variables enable you to separate deployment settings from your source code. For example, instead of hardcoding a database password, you can store this in an environment variable which you reference in your source code. [Learn more...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Step 6: Use the database locally
{: #use_database}

We're now going to update your local code to point to this database. We'll store the credentials for the services in a json file. This file will get used ONLY when the application is running locally. When running in {{site.data.keyword.Bluemix_notm}}, the credentials will be read from the VCAP_SERVICES environment variable.

1. Create the file src/GetStartedDotnet/vcap-local.json

2. In your browser, go to the {{site.data.keyword.Bluemix_notm}} dashboard and select **_your app_ > Connections**. Click the {{site.data.keyword.cloudant_short_notm}} menu icon (**&vellip;**) and select **View credentials**.

3. Copy and paste the entire json object from the credentials to the `vcap-local.json` file and save the changes.  The result will be something like:
  ```
  {
  "cleardb": [
    {
      "credentials": {
        ...
        "uri": "mysql://user:password@some-hostname.cleardb.net:3306/database-name?reconnect=true",
        ...
      },
      ...
      "name": "My ClearDB service instance name",
      ...
    }
  ]
}
  ```

4. From the `get-started-aspnet-core/src/GetStartedDotnet` directory restart your application with the 	`dotnet run` command.

  Refresh your browser view at: http://localhost:5000/. Any names you enter into the app will now get added to the database.

  Your local app and the {{site.data.keyword.Bluemix_notm}} app are sharing the database.  View your {{site.data.keyword.Bluemix_notm}} app at the URL listed in the output of the push command from above.  Names you add from either app should appear in both when you refresh the browsers.

Remember if you don't need your app live, stop it so you don't incur any unexpected charges.
{: tip}

## Next Steps

* [Tutorials](/docs/tutorials/index.html)
* [Samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
