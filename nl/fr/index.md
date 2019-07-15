---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}

L'environnement d'exécution Tomcat sur {{site.data.keyword.Bluemix}} repose sur le pack java_buildpack.
{: shortdesc}

Pour utiliser l'environnement d'exécution Tomcat sur {{site.data.keyword.Bluemix_notm}}, vous devez spécifier le pack java_buildpack avec l'option `-b`. Par exemple :

```
ibmcloud cf push <myApp> -p <pathToMyApp> -b java_buildpack
```

Pour plus d'informations sur l'environnement d'exécution Tomcat, voir le fichier [Readme java-buildpack](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md).

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} propose une application de démarrage Tomcat.  L'application de démarrage Tomcat est une application Tomcat simple qui fournit un modèle que vous pouvez utiliser. Vous pouvez expérimenter cette application et effectuer des modifications puis les envoyer par commande push vers l'environnement {{site.data.keyword.Bluemix_notm}}. Voir [Utilisation des applications de démarrage](../common/starter_app_usage.html) pour obtenir de l'aide.

## Versions d'environnement d'exécution
{: #runtime_versions}

Vous pouvez modifier la version de Tomcat que votre application doit utiliser en utilisant la variable d'environnement JBP_CONFIG_TOMCAT.
Vous pouvez modifier la version de Java que votre application doit utiliser en utilisant la variable d'environnement JBP_CONFIG_OPEN_JDK_JRE.
Ces deux variables d'environnement peuvent être définies dans le fichier manifeste de l'application.  Par exemple :
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.8.0_+ }}'
```
{: codeblock}
La version java_buildpack actuelle, v4.9, contient la version Tomcat 8.5.28 par défaut et la version Java 1.8.0_162 par défaut.
Pour plus d'informations, voir les informations sur les [éditions java-buildpack](https://github.com/cloudfoundry/java-buildpack/releases/tag/v4.9).

## Redirection HTTPS
{: #https_redirect}

L'environnement d'exécution Tomcat peut être configuré pour faire confiance aux proxy internes {{site.data.keyword.Bluemix_notm}} et autoriser la redirection du trafic HTTP vers HTTPS (SSL).
Pour ce faire, modifiez le fichier `server.xml` et définissez l'élément `RemoteIpValve` Valve avec les options `internalProxies` et `protocolHeader`.

Le fichier [server.xml](https://github.com/cloudfoundry/java-buildpack/blob/master/resources/tomcat/conf/server.xml) de l'environnement d'exécution Tomcat inclus dans le pack de construction ne définit par défaut que l'option `protocolHeader` pour l'élément `RemoteIpValve` Valve. Pour rediriger le trafic HTTP vers HTTPS dans {{site.data.keyword.Bluemix_notm}}, configurez l'élément `RemoteIpValve` dans le fichier `server.xml` personnalisé, comme illustré dans l'exemple suivant :

```
 <Valve className='org.apache.catalina.valves.RemoteIpValve' protocolHeader='x-forwarded-proto' internalProxies='.*' />
```
{: codeblock}

Vous trouverez davantage d'options de configuration de RemoteIpValve dans la [documentation Tomcat![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://tomcat.apache.org/tomcat-8.5-doc/api/org/apache/catalina/valves/RemoteIpValve.html).
