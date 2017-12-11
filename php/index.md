---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}

The PHP runtime on {{site.data.keyword.Bluemix}} is powered by the php_buildpack.
The php_buildpack provides a complete runtime environment for PHP
apps.
{: shortdesc}

The php_buildpack is used in the following conditions:
* Your app contains a composer.json file, or
* your app contains a *.php file, or
* your app defines a ${WEBDIR} variable in its [options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html) file, and that variable is set to an existing directory within your app.

## Starter application
{: #starter_application}

{{site.data.keyword.Bluemix}} provides a PHP starter app.  The PHP starter application is a simple PHP app that provides a template that you can use for your app. You can experiment with the starter app, and make and push changes to the {{site.data.keyword.Bluemix}}
environment.  See [Using the starter applications](/docs/cfapps/starter_app_usage.html) for help with using the starter app.

## Enforce HTTPS on all pages in your application
{: #enforce_https}

To enforce using HTTPS instead of HTTP on all pages in your application when running in {{site.data.keyword.Bluemix_notm}} using Apache, the following changes need to be made to your ".htaccess" file.  This rule will apply to any request which was not made using HTTPS only when running in {{site.data.keyword.Bluemix_notm}}.

```
RewriteCond %{HTTP:X-Forwarded-Proto} !=https [NC]
RewriteCond %{ENV:BLUEMIX_REGION} !^$
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

## Runtime versions
{: #runtime_versions}

You can specify the version of PHP to be used by your app in the composer.json file. For example:

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
For more information, see [Composer Package links  ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://getcomposer.org/doc/04-schema.md#package-links).

When a version is not specified, version 5.5.38 is chosen by default.

### Available versions:
{: #available_versions}

The following PHP versions are available in the
[PHP buildpack](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.27)
currently installed in {{site.data.keyword.Bluemix}}:

* 5.5.37
* 5.5.38
* 5.6.29
* 5.6.30
* 7.0.14
* 7.0.15
* 7.1.0
* 7.1.1

If your app requires a PHP version that is not listed,
you can use the external
[PHP buildpack](https://github.com/cloudfoundry/php-buildpack.git) to
deploy the app.

# rellinks
{: #rellinks notoc}
## Tutorials and Samples
{: #samples notoc}
* [Build and deploy a REST API](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Build and deploy a mobile-friendly calorie counter](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## general
{: #general notoc}
* [Cloud Foundry buildpack for PHP](https://github.com/cloudfoundry/php-buildpack.git)
