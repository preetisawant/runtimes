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

El tiempo de ejecución de Tomcat en {{site.data.keyword.Bluemix}} está basado en el java_buildpack.
{: shortdesc}

Para utilizar el tiempo de ejecución en {{site.data.keyword.Bluemix_notm}}, debe especificar java_buildpack con la opción `-b`. Por ejemplo:

```
ibmcloud cf push <myApp> -p <pathToMyApp> -b java_buildpack
```

Para obtener más información sobre el tiempo de ejecución de Tomcat, consulte el
[java-buildpack readme](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md).

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} proporciona una aplicación de inicio de Tomcat.  La aplicación de inicio de Tomcat es una app de Tomcat sencilla que proporciona una plantilla que puede utilizar. Puede experimentar con la app de iniciador, y realizar y enviar por push cambios en el entorno de {{site.data.keyword.Bluemix_notm}}. Consulte [Utilización de las aplicaciones de inicio](../common/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede cambiar la versión de Tomcat que utilizará la app con la variable de entorno JBP_CONFIG_TOMCAT.
Puede cambiar la versión de Java que utilizará la app con la variable de entorno JBP_CONFIG_OPEN_JDK_JRE.
Ambos se pueden especificar en el archivo de manifiesto de la aplicación.  Por ejemplo:
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.8.0_+ }}'
```
{: codeblock}
La versión actual de java_buildpack es v4.9, que contiene la versión predeterminada 8.5.28 de Tomcat y la versión predeterminada 1.8.0_162 de Java.
Para obtener más información, consulte los releases [java-buildpack](https://github.com/cloudfoundry/java-buildpack/releases/tag/v4.9).

## Redirección de HTTPS
{: #https_redirect}

El tiempo de ejecución de Tomcat se puede configurar de modo que confíe en los proxies internos de {{site.data.keyword.Bluemix_notm}} y permita la redirección del tráfico HTTP a HTTPS (SSL).
Para ello, modifique el archivo `server.xml`, estableciendo el elemento `RemoteIpValve` Valve con las opciones `internalProxies` y `protocolHeader`.

El tiempo de ejecución Tomcat [server.xml](https://github.com/cloudfoundry/java-buildpack/blob/master/resources/tomcat/conf/server.xml) incluido en el paquete de compilación solo establece la opción `protocolHeader` del elemento `RemoteIpValve` de forma predeterminada.  Para redirigir el tráfico HTTP a HTTPS en {{site.data.keyword.Bluemix_notm}}, configure el elemento `RemoteIpValve` en su `server.xml` personalizado como se muestra en el siguiente ejemplo:

```
 <Valve className='org.apache.catalina.valves.RemoteIpValve' protocolHeader='x-forwarded-proto' internalProxies='.*' />
```
{: codeblock}

Encontrará más opciones de configuración para RemoteIpValve en la [documentación de Tomcat ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://tomcat.apache.org/tomcat-8.5-doc/api/org/apache/catalina/valves/RemoteIpValve.html).
