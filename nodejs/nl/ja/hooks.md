---

copyright:
  years: 2018
lastupdated: "2018-11-09"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# フックを使用したサード・パーティー・サービスの統合
{: #hooks}

フックを使用することで、SDK for Node.js ビルドパックでサード・パーティー・サービスを簡単に統合できます。お客様が統合するサード・パーティー・サービスに関するサポートは IBM では提供されないことに注意してください。サポートについて詳しくは、『[サード・パーティー・サービス](../common/buildpackSupport.html#third-party)』を参照してください。

SDK for Node.js ビルドパックには Dynatrace フックが含まれています。Dynatrace は、Node.js アプリケーションのアプリケーション・モニタリングを使用可能にします。ビルドパック内の Dynatrace フックの使用について詳しくは、[Dynatrace 資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")]( https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/application-only/deploy-oneagent-on-cloud-foundry-for-application-only-monitoring/){: new_window} を参照してください。


サード・パーティー資料に記述されている手順に従うときには、{{site.data.keyword.Bluemix_notm}} ビルドパックに対するコマンドを実行するために `cf` の代わりに `ibmcloud cf` コマンドを使用するように注意してください。
{: tip}
