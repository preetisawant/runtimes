---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Cloud Runtime for Swift
{: #swift_runtime}

The Runtime for Swift on {{site.data.keyword.Bluemix}} is powered by the [{{site.data.keyword.Bluemix_notm}} buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack) (i.e. swift_buildpack).
This buildpack provides a complete runtime environment for Swift applications.
{: shortdesc}

## Starter application
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} provides a Kitura-based Swift [starter application ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Cloud/Kitura-Starter). The Kitura starter app is a simple Swift app that you can use to learn about the types of server applications you can develop by using the Swift programming language. This sample app creates a basic Kitura HTTP server that returns HTML content to the client.

**Note:** The Kitura starter app is meant to be used for educational purposes. You can experiment with the starter app by making enhancements, and push those changes to the {{site.data.keyword.Bluemix_notm}} environment. See [Using the starter applications](../common/starter_app_usage.html) for help with using the starter application.

## Renaming your app
{: #renaming_your_app}

If you want to rename your app, either from the Kitura starter, or more generally, there are a few changes that need to be addressed. This will both avoid confusion, and ensure an error-free deployment.

- Rename the app's project folder to match your app's name.
- `Package.swift` - Change the following entries:
    - `name` - Should match the app's name.
    - `targets[Target(name:)]` - Should match the app's name.
- `manifest.yml` - Change following entries:
    - `name` - Should match the app's name.
    - `command` - The name of the executable to start your app (should match the name specified in the Package.swift file).

## Runtime versions
{: #runtime_versions}

The [Runtime for Swift ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Swift/swift-buildpack) (swift_buildpack) hosted on {{site.data.keyword.Bluemix_notm}} is updated to use the latest GA version of the Swift binaries. This is the recommended version of Swift to use in your app. The buildpack does list other Swift versions within its [manifest.yml ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) file, which are cached in the buildpack to provide reduced provisioning time.

If you'd like to use a different version of Swift on {{site.data.keyword.Bluemix_notm}} for your application, you can specify the version with a `.swift-version` file in the root of your repository. This `.swift-version` file defines which Swift version is to be used by the swift_buildpack.

```
$ cat .swift-version
4.1.2
```
{: pre}

Because there are frequent Swift language updates, you should always include a `.swift-version` file so that your app is "pinned" to the Swift version your application is known to work with.

Please note that you can specify any valid version of Swift in your `.swift-version` file. These alternate versions must match the naming from [Swift.org ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://swift.org/download/), from which they are directly downloaded. While using a non-cache version will take a bit longer to provision, there is no runtime performance difference of your Swift app.

The default swift_buildpack in {{site.data.keyword.Bluemix_notm}} is used if your app's root directory contains a `Package.swift` file.  If you'd like to use use an alternate buildpack, you must specify this by adding a `buildpack: {buildpackUrl}` entry to your app's manifest.yml file. Alternatively, you can define this at deployment time, using the `ibmcloud cf push -b {buildpackUrl}` command argument.


## Developer environments

Developers have several options when creating server-side applications with Swift. Those using an Apple macOS device might prefer to use the Xcode IDE, although this is not a requirement.  Swift-based apps that will be deployed and run on {{site.data.keyword.Bluemix_notm}} can use any programming editor or IDE.  Syntax highlighting and linting for Swift are available for many popular editors. The Swift REPL command line tool included in the binaries from [Swift.org ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://swift.org/), allow for local compilation and testing prior to deployment to {{site.data.keyword.Bluemix_notm}}.

For macOS users, you can use the [Kitura App ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.kitura.io/app.html) which simplifies the creation, deployment, management, and control of server-side Swift apps running on {{site.data.keyword.Bluemix_notm}}.  


## Enhanced integration

Working with the [Kitura web framework](http://ibm-swift.github.io/Kitura/) provides a great deal of capabilities. Kitura is modular in nature, and you will soon want to extend its functionality with packaged SDKs, to provide features such as authentication, access to Watson based services, and a wide variety of databases.  Kitura provides support for many databases directly, while other open source projects also provide SDKs for many database platforms. The following is a non-exhaustive list of SDKs provided by Kitura to work with external resources.

- [IBM Watson Developer Cloud Swift SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/swift-sdk/)
- [SwiftMetrics ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/RuntimeTools/SwiftMetrics)
- [IBM Cloudant and CouchDB ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Swift/Kitura-CouchDB)
- [KituraKit ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Swift/KituraKit)
- [Swift Kuery ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/Swift-Kuery/)
- [Swift Kuery ORM ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Swift/Swift-Kuery-ORM)

To find more Swift packages to include in your application, go to the Packages section of [Kitura.io](https://www.kitura.io/packages.html). Packages can be added to a Swift application by including the package's Git URL and version details into the app's `Package.swift` file. For more details on package management, refer to the [Package Manager section of Swift.org](https://swift.org/package-manager/).


## Related information

There are also other online tools available from IBM for the Swift developer.
- [IBM Swift DevCenter ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/swift/) - Main landing site for all IBM Swift information. You can find information on our offerings, blogs, social events, documentation, and more.
- [Kitura.io ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.kitura.io/index.html) provides news, samples, and resources for building Kitura applications.
- [Swift@IBM Slack ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://swift-at-ibm-slack.mybluemix.net/) provides forums for asking questions and solving problems with the Swift@IBM team.
