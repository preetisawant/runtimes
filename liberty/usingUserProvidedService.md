---

copyright:
  years: 2017, 2018
lastupdated: "2018-6-26"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Using a User-Provided Service with Liberty in {{site.data.keyword.cloud_notm}}
{: #using_user_provided}

Cloud Foundry provides a mechanism to connect to and use services which
are not necessarily provided by or available within your {{site.data.keyword.Bluemix_notm}} environment.
That facility is [User-Provided services](https://docs.cloudfoundry.org/devguide/services/user-provided.html).

This document presumes that:
  * you have a some service available,
  * you can obtain credentials for that service,
and describes the steps needed to connect to and use that service with the example
Getting-Started-Liberty sample application

For this discussion we will use the CloudantNoSQLDB instance as our example service,
and create a user-provided service to connect to it.

## Step 1: Push the Getting-Started application
{: #follow_getting_started}

Follow the steps in the [Getting started tutorial](/docs/runtimes/liberty/getting-started.html) up through pushing
the application to {{site.data.keyword.Bluemix_notm}}.  Stop before connecting the database.

## Step 2: Create a CloudantNoSQLDB instance
{: #create_cloudantnosqldb}

Follow the steps in the [Getting started tutorial](/docs/runtimes/liberty/getting-started.html) to
create a CloudantNoSqLDB instance

Use the view credentials option to copy the credentials from the CloudandNoSQLDB. Save those credentials in a local file, for example, cloudant-creds.

## Step 3: Create a user-provided service
To work with the Getting-Started application,
the name of the user provided service must contain
"cloudantNoSQLDB".  The Getting-Started application is
parsing the VCAP services variable and looking for
a user-provided service with a name that contains "cloudantNoSQLDB".

        ibmcloud cf cups my-cloudantNoSQLDB-ups -p cloudant-creds

## Step 4: Bind the user-provided service and restage the app
Bind the user-provided service to the getting-started application.

        ibmcloud cf bs GettingStartedLiberty my-cloudantNoSQLDB-ups

        ibmcloud cf restage GettingStartedLiberty

## Step 5: Confirm
Browse to you application and confirm that you
can add multiple names to the 'name' field.
