---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Node.js
{: #nodejs_runtime}

{{site.data.keyword.Bluemix}} の Node.js ランタイムには sdk-for-nodejs ビルドパックが採用されています。
sdk-for-nodejs ビルドパックは、Node.js アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

sdk-for-nodejs ビルドパックは、アプリケーションのルート・ディレクトリーに **package.json** ファイルが含まれている場合に使用されます。

アプリケーションは、PORT 環境変数を介して割り当てられたポート上で listen する必要があります。
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} には、Node.js スターター・アプリケーションが用意されています。  Node.js スターター・アプリケーションは、アプリケーションで使用可能なテンプレートを提供する、シンプルな Node.js アプリケーションです。 スターター・アプリケーションを試し、{{site.data.keyword.Bluemix_notm}} 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](../common/starter_app_usage.html)を参照してください。

## アプリケーション管理
{: #app_management}
{{site.data.keyword.Bluemix_notm}} には、Node.js アプリケーションを管理およびデバッグするために数多くのユーティリティーが用意されています。  詳しくは、[『アプリケーション管理』](../common/app_mng.html)を参照してください。

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Node.js ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://nodejs.org)
* [IBM API Connect](https://strongloop.com/)
