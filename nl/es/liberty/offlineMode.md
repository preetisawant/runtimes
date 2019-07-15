---

copyright:
  years: 2016, 2018
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Utilizar el modo fuera de línea para Liberty
{: #offline_mode}

Cuando una aplicación de Liberty se envía por push a {{site.data.keyword.Bluemix}}, el paquete de compilación de Liberty puede acceder a sitios externos a {{site.data.keyword.Bluemix_notm}} para adquirir artefactos que la aplicación necesita.  A continuación se muestran los sitios externos a los que puede acceder el paquete de compilación de Liberty.  En entornos [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) y
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) es posible que los sitios necesiten incluirse en una *lista blanca*.

* https://download.run.pivotal.io y https://java-buildpack.cloudfoundry.org se utilizan para acceder a componentes para:
  * [Agente AppDynamics ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.appdynamics.com/)
  * [Controlador JDBC MariaDB ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://mariadb.com/)
  * [Agente New Relic](newRelic.html)
  * [OpenJDK](customizingJRE.html#OpenJDK)
  * [Controlador JDBC PostgreSQL ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ se utiliza para acceder a componentes para [JRebel ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://zeroturnaround.com/software/jrebel/).
* https://download.ruxit.com/agent/paas/cloudfoundry/java se utiliza para acceder a componentes para el [Agente de Dynatrace Ruxit](dynatrace.html).
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/ se utiliza para acceder al [Agente de Dynatrace](dynatrace.html).

## Cómo trabajar con un proxy
{: #working_with_proxy}

En algunos entornos, como [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) y
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) se puede configurar un proxy. Consulte [Cómo trabajar con un proxy](/docs/runtimes/common/workingWithProxy.html) para obtener más detalles.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
