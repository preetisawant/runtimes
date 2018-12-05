---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"

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
