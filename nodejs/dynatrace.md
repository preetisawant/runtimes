---

copyright:
  years: 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Use Dynatrace to monitor Node.js in {{site.data.keyword.cloud_notm}}
{: #using_dynatrace}

Dynatrace is a third-party service that provides monitoring for your app. You can integrate Dynatrace with your Node.js application, but IBM does not provide support for third-party services. See [Third-party services](../common/buildpackSupport.html#third-party) for more information.

For information about Dynatrace and its licensing, see [Dynatrace Application Monitoring ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.dynatrace.com/en/products/application-monitoring.html).

When your Node.js application is configured to use Dynatrace, the Node.js runtime acquires a Dynatrace platform as a service (PaaS) installation script from a Dynatrace site and runs that Dynatrace agent with your app. To integrate Dynatrace with your app, you need to create a user-provided service and then bind the service to your app.

## Integrating Dynatrace with your application

1. Log in to your Dynatrace account, and generate a PaaS token. For details, see the [Generate PaaS token ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/how-do-i-monitor-cloud-foundry-applications/) section in the Dynatrace Cloud Foundry app monitoring documentation.

  Make note of your environment ID and token.
1. Create a user-provided service that points to your Dynatrace credentials by running the following command. The name of the service must contain the string `dynatrace`, such as `dynatrace-service`.

    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken"
    ```
    {: codeblock}
    
    **Note:** Do not replace `environmentid` or `apitoken` with your credentials. After you run the command, you will be prompted for their values.

    If you are using Dynatrace Managed, also add the `apiurl` field, which specifies the API endpoint of your Managed Server.
    
    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken, apiurl"
    ```
    {: codeblock}
    
    When prompted after you run the command, set the `apiurl` to `https://<YourManagedServerURL>/e/<environmentID>/api`.
    
1. After you push your app to {{site.data.keyword.Bluemix_notm}}, bind the user-provided service that you created to the app. For example, use the following command:
    ```
    ibmcloud cf bs myApp dynatrace-service
    ```
    {: codeblock}

    **Note**: You must restage your application after binding the service.

   Alternatively, you can bind the service to your app by adding the name of your user-provided service to the `service` section of your app's `manifest.yml` file.
   ```yaml
   ---
    applications:
    - path: .
      memory: 256M
      instances: 1
      name: myApp
      host: myApp
      disk_quota: 1024M
    services:
      - dynatrace-service
   ```
   {: codeblock}
