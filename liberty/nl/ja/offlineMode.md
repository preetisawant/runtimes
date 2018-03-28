---

copyright:
  years: 2016, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Liberty のオフライン・モードの使用
{: #offline_mode}

Liberty アプリケーションが {{site.data.keyword.Bluemix}} にプッシュされると、Liberty ビルドパックは {{site.data.keyword.Bluemix_notm}} の外部のサイトにアクセスして、このアプリケーションに必要な成果物を取得できます。  Liberty ビルドパックによるアクセスが可能な外部サイトを以下に示します。  [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 環境と [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) 環境では、これらのサイトが*ホワイトリスト*に登録されていなければならないことがあります。

* https://download.run.pivotal.io および https://java-buildpack.cloudfoundry.org を使用して、以下を対象とするコンポーネントにアクセスします。
  * [AppDynamics エージェント ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.appdynamics.com/)
  * [MariaDB JDBC ドライバー ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mariadb.com/)
  * [New Relic エージェント](newRelic.html)
  * [OpenJDK](customizingJRE.html#OpenJDK)
  * [PostgreSQL JDBC ドライバー ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ を使用して、[JRebel ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://zeroturnaround.com/software/jrebel/) のコンポーネントにアクセスします。
* https://download.ruxit.com/agent/paas/cloudfoundry/java を使用して、[Dynatrace Ruxit エージェント](dynatrace.html)のコンポーネントにアクセスします。
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/ を使用して、[Dynatrace エージェント](dynatrace.html)のコンポーネントにアクセスします。

## プロキシーの処理
{: #working_with_proxy}

[{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) や [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) などの一部の環境では、プロキシーを構成できます。 詳しくは、[『プロキシーの処理』](/docs/runtimes/common/workingWithProxy.html)を参照してください。

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
