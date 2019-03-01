---

copyright:
  years: 2016, 2018
lastupdated: "2018-11-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Utilizza la modalità offline per Liberty
{: #offline_mode}

Quando viene eseguito il push di un'applicazione Liberty a {{site.data.keyword.Bluemix}}, il pacchetto di build Liberty può accedere a siti esterni a {{site.data.keyword.Bluemix_notm}} per acquisire le risorse richieste dall'applicazione.  I seguenti sono dei siti esterni a cui può accedere il pacchetto di build Liberty.  Negli ambienti [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) e
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), è possibile che occorra che questi siti siano *inseriti in whitelist*.

* https://download.run.pivotal.io e https://java-buildpack.cloudfoundry.org sono utilizzati per accedere ai componenti di:
  * [AppDynamics agent ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.appdynamics.com/)
  * [MariaDB JDBC driver ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mariadb.com/)
  * [New Relic agent](/docs/runtimes/liberty/monitoring/newRelic.html)
  * [OpenJDK ](/docs/runtimes/liberty/customizingJRE.html#OpenJDK)
  * [PostgreSQL JDBC driver ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ è utilizzato per accedere ai componenti di [JRebel ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://zeroturnaround.com/software/jrebel/).
* https://download.ruxit.com/agent/paas/cloudfoundry/java è utilizzato per accedere ai componenti di [Dynatrace Ruxit agent](dynatrace.html).
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/  è utilizzato per accedere a [Dynatrace agent](dynatrace.html).

## Utilizzo di un proxy
{: #working_with_proxy}

In alcuni ambienti, come ad esempio [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) e
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), può essere configurato un proxy. Consulta
[Gestione di un proxy](/docs/runtimes-common/workingWithProxy.html) per ulteriori dettagli.
