---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-08"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Use the beta features
{: #using_beta_features}

The Liberty beta features provide early access to new functionality and programming models that might be included in a future Liberty release. Most of the beta features can also be used in applications deployed to {{site.data.keyword.Bluemix}}.

**Important**: The beta features are for development and test purposes only and cannot be used in production. For the complete terms of use, see the [beta license agreement](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

| Features |
| ------ |
| `appSecurity-3.0` |
| `audit-1.0` |
| `beanValidation-2.0` |
| `cdi-2.0` |
| `javaee-8.0` |
| `javaeeClient-8.0` |
| `jaxrs-2.1` |
| `jpa-2.2` |
| `jpaContainer-2.2` |
| `jsf-2.3` |
| `jsfContainer-2.3` |
| `jsonb-1.0` |
| `jsonbContainer-1.0` |
| `jsonp-1.1` |
| `jsonpContainer-1.1` |
| `logstashCollector-1.1` |
| `servlet-4.0` |
| `usageMetering-1.0` |
| `validator-1.0` |
| `webProfile-8.0` |
{: caption="Table 1. Liberty Beta features available in Liberty for Java in {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

To use the Liberty beta features in {{site.data.keyword.Bluemix_notm}}, you will need to do the following:

1. [Deploy a server directory or a packaged server](optionsForPushing.html) with one or more beta features enabled in the server.xml file as in the example that follows:

  ```
<server>
    <featureManager>
        <feature>servlet-4.0</feature>
        <feature>webProfile-8.0</feature>
    </featureManager>
</server>
  ```
  {: .codeblock}

2.  Set the `IBM_LIBERTY_BETA` environment variable to `true`. This variable directs the Liberty buildpack to install and enable the beta features for your application.  For example:
  * Using the `cf` command line tool:
    ```
    cf set-env <yourappname> IBM_LIBERTY_BETA true
    ```
    {: .codeblock}

  * Or, using the `manifest.yml` file:
    ```
      env:
          IBM_LIBERTY_BETA: "true"
    ```
    {: .codeblock}

3. Set the `JBP_CONFIG_LIBERTY` environment variable to `"version: +"`. This variable enables the [Liberty monthly runtime](buildpackDefaults.html#liberty_versions), which supports beta features. For example:
  * Using the `cf` command line tool:
    ```
    cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ```
    {: .codeblock}

  * Or, using the `manifest.yml` file:
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
    ```
    {: .codeblock}

If you are enabling the beta features on an existing application, don't forget to re-stage your application after you set the environment variables.
