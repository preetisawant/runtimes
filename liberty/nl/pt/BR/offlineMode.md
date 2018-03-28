---

copyright:
  years: 2016, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Use o modo off-line para o Liberty
{: #offline_mode}

Quando um aplicativo Liberty é enviado por push para {{site.data.keyword.Bluemix}}, o buildpack do Liberty pode acessar
sites externos ao {{site.data.keyword.Bluemix_notm}} para adquirir os artefatos requeridos pelo aplicativo.  Veja a seguir os sites externos que o buildpack do Liberty pode acessar.  Em ambientes [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) e
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), estes sites podem
precisar ser *incluídos na lista de desbloqueio*.

* https://download.run.pivotal.io e https://java-buildpack.cloudfoundry.org são usados para acessar componentes para:
  * [Agente AppDynamics ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.appdynamics.com/)
  * [Driver JDBC MariaDB ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://mariadb.com/)
  * [Agente New Relic](newRelic.html)
  * [OpenJDK](customizingJRE.html#OpenJDK)
  * [Driver JDBC PostgreSQL ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ é usado para acessar componentes para o [JRebel ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://zeroturnaround.com/software/jrebel/).
* https://download.ruxit.com/agent/paas/cloudfoundry/java é usado para acessar componentes para o [agente Dynatrace Ruxit](dynatrace.html).
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/ é usado para acessar o [agente Dynatrace](dynatrace.html).

## Trabalhando com um proxy
{: #working_with_proxy}

Em alguns ambientes, como [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) e [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), um proxy pode ser configurado. Consulte
[Trabalhando com um proxy](/docs/runtimes/common/workingWithProxy.html) para obter mais detalhes.

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
