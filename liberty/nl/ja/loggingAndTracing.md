---

copyright:
  years: 2015, 2018
lastupdated: "2018-1-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ロギングおよびトレースの構成
{: #logging_tracing}

## ログ・ファイル
{: #log_files}

標準 Liberty ログ (`messages.log` や `ffdc` ディレクトリーなど) が {{site.data.keyword.Bluemix}} で使用可能であり、各アプリケーション・インスタンスの `logs` ディレクトリーにあります。 これらのログには、{{site.data.keyword.Bluemix_notm}} コンソールからアクセスすることも、Cloud Foundry CLI を使用してアクセスすることもできます。 例えば、次のとおりです。

* アプリケーションの最新のログにアクセスするには、以下のコマンドを実行します。

  ```
  cf logs --recent <appname>
  ```
  {: codeblock}


* アプリケーションの `messages.log` ファイルを表示するには、以下のコマンドを実行します。

  ```
  cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

ログ・レベルおよびその他のトレース・オプションは、Liberty 構成ファイルで設定できます。 詳しくは、[『Liberty のトラブルシューティング: ロギングおよびトレース』](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)を参照してください。

## トレース機能およびダンプ機能の使用
{: #using_trace_and_dump}

### {{site.data.keyword.Bluemix_notm}} コンソールでのトレースとダンプの使用 (非推奨)

実行中のアプリケーションに関する Liberty トレース構成は、{{site.data.keyword.Bluemix_notm}} コンソールから直接調整できます。 コンソールには、スレッド・ダンプおよびヒープ・ダンプの要求およびダウンロードを行う機能もあります。 トレース構成を調整したりダンプを要求したりするには、{{site.data.keyword.Bluemix_notm}} コンソールで Liberty アプリケーションを選択して、ナビゲーションで`「ランタイム」`メニューを選択します。 `「ランタイム」`ビューで、インスタンスを選択し、*「トレース」*ボタンまたは*「ダンプ」*ボタンを押します。 トレース・レベルを調整する場合のトレース仕様の構文の詳細については、[『Liberty のトラブルシューティング: ロギングおよびトレース』](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)を参照してください。

### SSH を介したトレース構成の変更

アプリケーションをプッシュすると、デフォルト・プロパティーの **updateTrigger** は **polled** に、**monitorInterval** は 1 分に設定されて、server.xml ファイルに含まれています。Liberty サーバーは、server.xml の更新を 1 分ごとにチェックするよう、自動的に構成されます。

カスタマイズされた sever.xml を含む Liberty アプリケーションをプッシュするためのオプションについては、[『server.xml を含む Liberty アプリケーションのプッシュ』](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing)を参照してください。

server.xml での動的更新のセットアップ方法については、[『動的更新の制御』](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window}を参照してください。

トレース構成を変更するには、以下の手順を実行します。

1. SSH 経由でアプリケーションに接続します。

  ```
 cf ssh <appname> [-i instance_index]
  ```
  {: codeblock}

2. 以下のように server.xml 内の ```<logging traceSpecification="xxxx"/>``` を編集して、必要なトレース指定 (例えば、*vi* を使用) を設定します。

  ```
vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: codeblock}

注: server.xml の変更は、再ステージング時または再始動時に失われます。SSH で接続中のインスタンスにのみ有効です。

トレース仕様の構文の詳細については、[『Liberty のトラブルシューティング: ロギングおよびトレース』](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window}を参照してください。

### SSH を介したダンプのトリガー

SSH フィーチャーを使用して CF CLI を介してスレッド・ダンプおよびヒープ・ダンプをトリガーするには、以下のコマンドを使用します。

  ```
 cf ssh <appname> -c "pkill -3 java"
  ```
  {: codeblock}

生成されたダンプ・ファイルのダウンロードについて詳しくは、以下の説明を参照してください。

## ダンプ・ファイルのダウンロード
{: #download_dumps}

デフォルトでは、各種ダンプ・ファイルはアプリケーション・コンテナーの `dumps` ディレクトリーに置かれます。ダンプ・ファイルの表示およびダウンロードには、Cloud Foundry CLI の `cf ssh` を使用します。

* 生成されたダンプを表示するには、以下のコマンドを実行します。

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* ダンプ・ファイルをダウンロードするには、以下のコマンドを実行します。

  ```
  cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

`scp` およびその他の類似ツールを使用してダンプ・ファイルの表示およびダウンロードを行うことも可能です。 詳しくは、[SSH を使用したアプリケーションへのアクセス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) を参照してください。

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Liberty ランタイム](index.html)
* [Liberty の概要](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
