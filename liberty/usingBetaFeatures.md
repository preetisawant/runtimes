---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Use the beta features
{: #using_beta_features}

The Liberty beta features provide early access to new functionality and programming models that might be included in a future Liberty release. Most of the beta features can also be used in applications deployed to {{site.data.keyword.Bluemix}}.

**Important**: The beta features are for development and test purposes only and may not be used in production. For the complete terms of use please see the [beta license agreement](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

Liberty beta features available in {{site.data.keyword.Bluemix_notm}}
<table>
<tr>
<th align="left">Features</th>
</tr>

<tr>
    <tr><td>appSecurity-3.0</tr></td>
    <tr><td>audit-1.0</tr></td>
    <tr><td>beanValidation-2.0</tr></td>
    <tr><td>bluemixLogCollector-1.1</tr></td>
    <tr><td>cdi-2.0</tr></td>
    <tr><td>javaee-8.0</tr></td>
    <tr><td>javaeeClient-8.0</tr></td>
    <tr><td>jaxrs-2.1</tr></td>
    <tr><td>jpa-2.2</tr></td>
    <tr><td>jpaContainer-2.2</tr></td>
    <tr><td>jsf-2.3</tr></td>
    <tr><td>jsfContainer-2.2</tr></td>
    <tr><td>jsonb-1.0</tr></td>
    <tr><td>jsonbContainer-1.0</tr></td>
    <tr><td>jsonp-1.1</tr></td>
    <tr><td>jsonpContainer-1.1</tr></td>
    <tr><td>logstashCollector-1.1</tr></td>
    <tr><td>mpConfig-1.2</tr></td>
    <tr><td>mpOpenAPI-1.0</tr></td>
    <tr><td>mpRestClient-1.0</tr></td>
    <tr><td>opentracing-1.0</tr></td>
    <tr><td>servlet-4.0</tr></td>
    <tr><td>validator-1.0</tr></td>
    <tr><td>webProfile-8.0</tr></td>

</tr>
</table>

In order to use the Liberty beta features in {{site.data.keyword.Bluemix_notm}} you will need to do following:

1. [Deploy a server directory or a packaged server](optionsForPushing.html) with one or more beta features enabled in the server.xml file as in the example that follows:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>mpOpenAPI-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Set the **IBM_LIBERTY_BETA** environment variable to **true**. This variable directs the Liberty buildpack to install and enable the beta features for your application.  For example:
  * using the cf command line tool:
```
       $ cf set-env <yourappname> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * or, using the manifest.yml file:
```
      env:
          IBM_LIBERTY_BETA: "true"
```

3. Set the **JBP_CONFIG_LIBERTY** environment variable to **"version: +"**. This variable enables the [Liberty monthly runtime](buildpackDefaults.html#liberty_versions) which supports beta features. For example:
  * using the cf command line tool:
```
       $ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * or, using the manifest.yml file:
```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
```

If you are enabling the beta features on an existing application, don't forget to re-stage your application after setting the environment variables.

{: #codeblock}

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Liberty for Java runtime](index.html)
* [Liberty Overview](https://www.ibm.com/support/knowledgecenter/SSAW57_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/cwlp_about.html)
