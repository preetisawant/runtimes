---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

{{site.data.keyword.Bluemix}} の Java アプリケーション用 Liberty には liberty-for-java ビルドパックが採用されています。 liberty-for-java ビルドパックは、WebSphere Liberty に加えて、Java EE 7 アプリケーションおよび OSGi アプリケーションを実行するための完全なランタイム環境を提供します。 また、Spring のような一般的なフレームワークをサポートし、{{site.data.keyword.IBM_notm}} JRE を含んでいます。 Liberty は素早いアプリケーション開発を可能にし、これはクラウドによく適しています。
{: shortdesc}

## 検出
{: #detection}
Liberty ビルドパックは、以下のような種類のアプリケーションがデプロイされた場合に使用されます。
* [WAR ファイル](optionsForPushing.html#stand_alone_apps)
* [EAR ファイル](optionsForPushing.html#stand_alone_apps)
* [Liberty サーバー・ディレクトリー](optionsForPushing.html#server_directory)
* [パッケージされた Liberty サーバー](optionsForPushing.html#packaged_server)
* Java メイン
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## スターター・アプリケーション
{: #starter_application}
{{site.data.keyword.Bluemix_notm}} には、いくつかの Liberty スターター・アプリケーションが用意されています。  Liberty スターター・アプリケーションは、使用可能なテンプレートを提供する、シンプルな Liberty アプリケーションです。 スターター・アプリケーションを試し、{{site.data.keyword.Bluemix_notm}} 環境に対して変更を行い、プッシュすることができます。  スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](../common/starter_app_usage.html)を参照してください。

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [Liberty アプリケーションの管理](../common/app_mng.html#Utilities)
* [IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} を使用したアプリのデプロイ](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [{{site.data.keyword.loganalysislong_notm}} の概説](/docs/services/CloudLogAnalysis/index.html)
* [{{site.data.keyword.prf_hublong}}](/docs/services/AvailabilityMonitoring/index.html) の概説
