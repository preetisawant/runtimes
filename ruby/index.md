---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Ruby
{: #ruby_runtime}

The Ruby runtime on {{site.data.keyword.Bluemix}} is powered by the ruby_buildpack.
The ruby_buildpack provides a complete runtime environment for Ruby apps.
{: shortdesc}

The ruby_buildpack is used if your app has a Gemfile in the root directory. It will then use Bundler to install your dependencies.

## Starter application
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} provides a Ruby starter application.  The Ruby starter application is a simple Ruby app that provides a template that you can use for your app. You can experiment with the starter app, and make and push changes to the  {{site.data.keyword.Bluemix_notm}}
environment.  See [Using the starter applications](../common/starter_app_usage.html) for help with using the starter application.

## Runtime versions
{: #runtime_versions}

You can specify the version of Ruby to be used by your app in your application's Gemfile, for example:

```
  source 'https://rubygems.org'
  ruby '2.4.1'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

When a version is not specified, version 2.4.3 is chosen by default.

### Available versions:
{: #available_versions}

The following Ruby versions are available in the
[Ruby buildpack](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.7.15)
currently installed in {{site.data.keyword.Bluemix}}:

* 2.2.8
* 2.2.9
* 2.3.5
* 2.3.6
* 2.4.2
* 2.4.3
* 2.5.0

If your app requires a Ruby version that is not listed,
you can use the external
[Ruby buildpack](https://github.com/cloudfoundry/ruby-buildpack) to
deploy the app.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Cloud Foundry buildpack for Ruby](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Ruby on Rails documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://api.rubyonrails.org/)
