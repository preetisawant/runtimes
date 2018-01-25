---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

Las aplicaciones Liberty for Java de {{site.data.keyword.Bluemix}} se basan en el paquete de compilación liberty-for-java. El paquete de compilación liberty-for-java proporciona un entorno de ejecución completo para la ejecución de aplicaciones Java EE 7 y OSGi sobre el perfil de Liberty. Admite infraestructuras extendidas, como Spring e incluye {{site.data.keyword.IBM_notm}} JRE. WebSphere Liberty permite desarrollar rápidamente aplicaciones adaptadas a la nube.
{: shortdesc}

## Detección
{: #detection}
El paquete de compilación de Liberty se utiliza cuando se despliegan los siguientes tipos de aplicaciones:
* [Archivos WAR](optionsForPushing.html#stand_alone_apps)
* [Archivos EAR](optionsForPushing.html#stand_alone_apps)
* [Directorio del servidor de Liberty](optionsForPushing.html#server_directory)
* [Servidor empaquetado de Liberty](optionsForPushing.html#packaged_server)
* Principal de Java
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## Aplicación de inicio
{: #starter_application}
{{site.data.keyword.Bluemix_notm}} proporciona varias aplicaciones de inicio de Liberty.  Las aplicaciones de inicio de Liberty son apps de Liberty sencillas que proporcionan una plantilla que puede utilizar. Puede experimentar con las apps de iniciador, y realizar y enviar por push cambios en el entorno de {{site.data.keyword.Bluemix_notm}}.  Consulte [Utilización de las aplicaciones de inicio](/docs/cfapps/starter_app_usage.html) para obtener ayuda con el uso de las aplicaciones de inicio.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [Gestión de apps de Liberty](/docs/manageapps/app_mng.html#Utilities)
* [Despliegue de apps con IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [Iniciación a IBM Monitoring and Analytics for {{site.data.keyword.Bluemix_notm}} Service](/docs/services/monana/index.html#monana_oview)
