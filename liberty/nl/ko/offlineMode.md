---

copyright:
  years: 2016, 2018
lastupdated: "2018-11-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Liberty의 오프라인 모드 사용
{: #offline_mode}

Liberty 애플리케이션이 {{site.data.keyword.Bluemix}}에 푸시되면 Liberty 빌드팩이 {{site.data.keyword.Bluemix_notm}}의 외부에 있는 사이트에 액세스하여
애플리케이션에 필요한 아티팩트를 가져올 수 있습니다. 다음은 Liberty 빌드팩이 액세스할 수 있는 외부 사이트입니다.  [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 및
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) 환경에서 이 사이트는 *화이트리스트에 추가*되어야 할 수 있습니다.

* 다음은 아래의 컴포넌트에 액세스하는 데 사용됩니다. https://download.run.pivotal.io 및 https://java-buildpack.cloudfoundry.org
  * [AppDynamics 에이전트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.appdynamics.com/)
  * [MariaDB JDBC 드라이버 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mariadb.com/)
  * [New Relic 에이전트](monitoring/newRelic.html)
  * [OpenJDK](customizingJRE.html#OpenJDK)
  * [PostgreSQL JDBC 드라이버 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/은 [JRebel ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://zeroturnaround.com/software/jrebel/)의 컴포넌트에 액세스하는 데 사용됩니다.
* 다음은 [Dynatrace Ruxit 에이전트](dynatrace.html)의 컴포넌트에 액세스하는 데 사용됩니다. https://download.ruxit.com/agent/paas/cloudfoundry/java
* 다음은 [Dynatrace 에이전트](dynatrace.html)에 액세스하는 데 사용됩니다. http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/

## 프록시 작업
{: #working_with_proxy}

[{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 및
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) 등의 일부 환경에서는 프록시의 구성이 가능합니다. 자세한 내용은
[프록시 작업](/docs/runtimes/common/workingWithProxy.html)을 참조하십시오.
