---

copyright:
  years: 2016, 2018
lastupdated: "2018-11-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Use o modo off-line para o Liberty
{: #offline_mode}

Quando um aplicativo Liberty é enviado por push para o {{site.data.keyword.Bluemix}}, o buildpack do Liberty pode acessar sites externos ao {{site.data.keyword.Bluemix_notm}} para adquirir artefatos requeridos pelo aplicativo.  Veja a seguir os sites externos que o buildpack do Liberty pode acessar.  Nos ambientes [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) e
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), esses sites podem precisar ser *incluídos na lista de desbloqueio*.

* https://download.run.pivotal.io e https://java-buildpack.cloudfoundry.org são usados para acessar componentes para:
  * [Agente AppDynamics ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.appdynamics.com/)
  * [Driver JDBC MariaDB ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://mariadb.com/)
  * [Agente New Relic](/docs/runtimes/liberty/monitoring/newRelic.html)
  * [OpenJDK ](/docs/runtimes/liberty/customizingJRE.html#OpenJDK)
  * [Driver JDBC PostgreSQL ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ é usado para acessar componentes para o [JRebel ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://zeroturnaround.com/software/jrebel/).
* https://download.ruxit.com/agent/paas/cloudfoundry/java é usado para acessar componentes para o [agente Dynatrace Ruxit](dynatrace.html).
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/ é usado para acessar o [agente Dynatrace](dynatrace.html).

## Trabalhando com um proxy
{: #working_with_proxy}

Em alguns ambientes, como o [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) e o [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), um proxy pode ser configurado. Consulte
[Trabalhando com um proxy](/docs/runtimes-common/workingWithProxy.html) para obter mais detalhes.
