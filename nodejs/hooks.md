---

copyright:
  years: 2018
lastupdated: "2018-11-09"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# Integrate third-party services using hooks
{: #hooks}

You can use hooks to easily integrate third-party services in the SDK for Node.js buildpack. Note that IBM does not provide support for any third-party services that you integrate. For more information about support, see [Third-party services](../common/buildpackSupport.html#third-party).

The SDK for Node.js buildpack includes the same hooks as the community buildpack.

* **Dynatrace**

   Dynatrace enables application monitoring of Node.js applications. Learn more about using the Dynatrace hook in the buildpack in the [Dynatrace documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")]( https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/application-only/deploy-oneagent-on-cloud-foundry-for-application-only-monitoring/){: new_window}.

* **Snyk**

   Snyk enables you to test and fix Node.js applications that manage their dependencies using either npm or Yarn. Learn more about using the Snyk hook in the buildpack in the [Snyk documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://snyk.io/docs/cloud-foundry){: new_window}.

When following instructions in third-party documentation, remember to use the `ibmcloud cf` command instead of `cf` to run commands for your {{site.data.keyword.Bluemix_notm}} buildpack.
{: tip}
