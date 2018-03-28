---

copyright:
  years: 2016, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Utiliser le mode hors ligne pour Liberty
{: #offline_mode}

Quand une application Liberty est poussée vers {{site.data.keyword.Bluemix}}, le pack de construction Liberty peut accéder à des sites externes à
{{site.data.keyword.Bluemix_notm}} afin d'obtenir les artefacts requis par l'application.  Les sites externes accessibles au pack de construction Liberty sont répertoriés ci-dessous.  Dans les environnements
[{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) et
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), ces sites peuvent avoir besoin d'être mis en *liste blanche*.

* https://download.run.pivotal.io et https://java-buildpack.cloudfoundry.org sont utilisés pour accéder aux composants pour :
  * [l'agent AppDynamics ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.appdynamics.com/)
  * [le pilote JDBC MariaDB ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mariadb.com/)
  * [l'agent New Relic](newRelic.html)
  * [OpenJDK](customizingJRE.html#OpenJDK)
  * [le pilote JDBC PostgreSQL ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ est utilisé pour accéder aux composants pour [JRebel ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://zeroturnaround.com/software/jrebel/).
* https://download.ruxit.com/agent/paas/cloudfoundry/java est utilisé pour accéder aux composants pour l'[agent Dynatrace Ruxit](dynatrace.html).
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/ est utilisé pour accéder à l'[agent Dynatrace](dynatrace.html).

## Utilisation d'un proxy
{: #working_with_proxy}

Dans certains environnements, comme [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) et
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), un proxy peut être configuré. Voir
[Utilisation d'un proxy](/docs/runtimes/common/workingWithProxy.html) pour plus de détails.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
