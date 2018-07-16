---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# バインドされたサービスの構成
{: #auto_config}

さまざまなサービスを Liberty for Java アプリケーションにバインドすることができます。 サービスは開発者の希望によって、コンテナー管理、アプリケーション管理、またはその両方にできます。

アプリケーション管理サービスとは、Liberty からの支援は何もなく、完全にアプリケーションによって管理されるサービスのことです。 アプリケーションは、通常、
VCAP_SERVICES を読み取って、バインドされたサービスについての情報を取得し、サービスに直接アクセスします。 必要なすべてのクライアント・アクセス・コードをアプリケーションが提供します。 Liberty フィーチャーまたは server.xml ファイル構成にはまったく依存しません。 このタイプのサービスには Liberty ビルドパックの自動構成は適用されません。

コンテナー管理サービスとは、Liberty ランタイムによって管理されるサービスのことです。 バインドされたサービスをアプリケーションが JNDI で検索する場合もあり、
サービスが Liberty 自体によって直接使用される場合もあります。 Liberty ビルドパックが VCAP_SERVICES を読み取って、
バインドされたサービスについての情報を取得します。 ビルドパックは、各コンテナー管理サービスに 3 つの機能を実行します。

* バインドされたサービス用の[クラウド変数](optionsForPushing.html#accessing_info_of_bound_services)を生成する。
* バインドされたサービスへのアクセスに必要な Liberty フィーチャーおよびクライアント・アクセス・コードをインストールする。
* サービスで要求される server.xml ファイル・スタンザを生成または更新する。

このプロセスは自動構成と呼ばれます。

Liberty ビルドパックは、以下のサービス・タイプに対して自動構成を提供します。

* [Auto-Scaling](/docs/services/Auto-Scaling/index.html#autoscaling)
* [ClearDB MySQL Database ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.cleardb.com/developers)
* [Cloudant NoSQL Database](/docs/services/Cloudant/index.html#Cloudant)
* [Compose for MongoDB](/docs/services/ComposeForMongoDB/index.html)
* [Compose for MySQL](/docs/services/ComposeForMySQL/index.html)
* [Compose for PostgreSQL](/docs/services/ComposeForPostgreSQL/index.html)
* [dashDB](/docs/services/dashDB/index.html#dashDB)
* [ElephantSQL](docs/services/ElephantSQL/index.html)
* [Single Sign On](/docs/services/SingleSignOn/index.html#sso_gettingstarted)

Compose サービスには、コンテナー管理またはアプリケーション管理のいずれかが可能です。 デフォルトでは、Liberty ビルドパックは、これらのサービスはコンテナー管理であると想定し、これらを自動的に構成します。 アプリケーションがサービスを管理するようにしたい場合、`services_autoconfig_excludes` 環境変数を設定することで、サービスの自動構成をオプトアウトできます。 詳しくは、[『サービス自動構成のオプトアウト』](autoConfig.html#opting_out)を参照してください。

## Liberty フィーチャーおよびクライアント・アクセス・コードのインストール
{: #installation_of_liberty_features}

コンテナー管理サービスにバインドする際、サービスによっては、server.xml ファイルの featureManager スタンザでの Liberty フィーチャーの構成が必要な場合もあります。 Liberty ビルドパックは featureManager スタンザを更新し、
サポートされている必要なバイナリーをインストールします。 サービスがクライアント・ドライバーの jar を必要とする場合、
jar が Liberty インストール済み環境の既知の場所にダウンロードされます。

バインドされたサービス・タイプについて詳しくは、[『サービス自動構成のオプトアウト』](#opting_out)セクションを参照してください。

## server.xml 構成スタンザの生成または更新
{: #generating_or_updating_serverxml}

アプリケーションのサービスへのバインド方法と既存の server.xml ファイルの有無によっては、スタンドアロン・アプリケーションをプッシュすると、Liberty ビルドパックが、server.xml ファイル内の構成スタンザを自動的に生成または更新することができます。

[『Liberty アプリケーションのプッシュのオプション』](optionsForPushing.html#options_for_pushing)に記述されているように、スタンドアロン・アプリケーションをプッシュすると、Liberty ビルドパックによって server.xml 構成スタンザが {{site.data.keyword.Bluemix_notm}} に生成されます。

スタンドアロン・アプリケーションをプッシュし、コンテナー管理サービスにバインドすると、それらのバインドされたサービスに必要な server.xml スタンザが Liberty ビルドパックによって生成されます。

server.xml ファイルを用意し、コンテナー管理サービスにバインドすると、Liberty ビルドパックによって、構成スタンザが生成または更新されます。

* 用意された server.xml ファイルに、バインドされたサービスの構成スタンザが含まれていない場合、Liberty は、バインドされたサービスの構成を生成します。
* 用意された server.xml ファイルに、バインドされたサービスの構成スタンザが含まれている場合、Liberty は、バインドされたサービスの構成を更新します。

詳細については、バインドされたサービスのタイプに関する資料を参照してください。

## サービス自動構成のオプトアウト
{: #opting_out}

場合によっては、
バインドしたサービスを Liberty ビルドパックが自動的に構成するのが望ましくないことがあります。 次のようなシナリオが考えられます。

* 自分のアプリケーションが *dashDB* を使用している場合に、このアプリケーションでデータベースへの接続を直接管理したい。 ア
プリケーションには、必要なクライアント・ドライバー jar が含まれている。 Liberty ビルドパックによる *dashDB* サービスの自動構成を望まない。
* server.xml ファイルを用意しているところであり、非標準データ・ソース構成が必要なため、*cloudant* インスタンス用の構成スタンザを作成した。 この server.xml ファイルを、Liberty ビルドパックによって更新されないようにしたいが、Liberty ビルドパックによって、サポートされている適切なソフトウェアが確実にインストールされるようにもしたい。

自動サービス構成をオプトアウトするには、
services_autoconfig_excludes 環境変数を使用します。 この環境変数を manifest.yml に組み込むか、または、{{site.data.keyword.Bluemix_notm}} クライアントを使用してこの環境変数を設定することができます。

サービス・タイプごとにサービスの自動構成をオプトアウトすることができます。 完全にオプトアウトする (上の *dashDB* シナリオ) か、または server.xml ファイル構成の更新のみをオプトアウトする (上の *cloudant* シナリオ) ことを選択できます。 services_autoconfig_excludes 環境変数に指定する値は、以下に示すようなストリングになります。

* このストリングは、1 つ以上のサービスのオプトアウト指定を含むことができます。
* 具体的なサービスのオプトアウト指定は、service_type=option で、それぞれの意味は次のとおりです。
  * service_type は、VCAP_SERVICES に表示される、サービスのラベルです。
  * option は、all または config のいずれかです。
* このストリングが複数のサービスのオプトアウト指定を含む場合、
個々のオプトアウト指定を 1 個の空白文字で区切る必要があります。

以下に示す services_autoconfig_excludes ストリングの文法の例を参照してください。

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type (service label as it appears in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: codeblock}

**重要**: 指定するサービス・タイプは、VCAP_SERVICES 環境変数内で表示されるサービス・ラベルと一致しなければなりません。 空白文字は使用できません。
**重要**: `<service_type_specification>` 内に空白文字を含めることはできません。 空白文字の使用が許可されるのは、複数の `<service_type_specification>` インスタンスを区切る場合のみです。

上記の *dashDB* シナリオのように、特定のサービスに対するすべての自動構成アクションをオプトアウトするには、**all** オプションを使用します。 上記の *cloudant* シナリオのように、構成の更新アクションのみをオプトアウトするには、**config** オプションを使用します。

以下に、*dashDB* シナリオと *cloudant* シナリオの manifest.yml ファイル内のオプトアウト指定の例を示します。

```
    env:
      services_autoconfig_excludes: dashDB=all

    env:
      services_autoconfig_excludes: cloudant=config

    env:
      services_autoconfig_excludes: cloudant=config dashDB=all
```
{: codeblock}

以下の例は、
コマンド・ライン・インターフェースを使用して、アプリケーションの myapp の services_autoconfig_excludes 環境変数を設定する方法を示します。

```
    ibmcloud cf set-env myapp services_autoconfig_excludes cloudant=config
    ibmcloud cf set-env myapp services_autoconfig_excludes "cloudant=config dashDB=all"
```
{: codeblock}

VCAP_SERVICES でサービスの *label* を検索するには、以下の例のようなコマンドを発行します。

```
    ibmcloud cf env myapp
```
{: codeblock}

出力には、以下のようなテキストが含まれています。ここで、**label** フィールドに値 **elephantsql** が示されています。

```
   "elephantsql": [
   {
      "credentials": {
      "max_conns": "5",
      "uri":      "..."
   },
   "label": "elephantsql",

```
{: codeblock}

## サービス構成のオーバーライド
{: #override_service_config}

場合によっては、自動構成で生成されたサービスのデフォルト構成をオーバーライドしたいことがあります。
**LBP_SERVICE_CONFIG_xxxx** 環境変数を使用して、サービスをオーバーライドすることができます。 環境変数の完全な名前と、オーバーライドの構文例については、以下の表を参照してください。  例えば、*elephantSQL* サービスのデフォルト・バージョンをオーバーライドしてバージョン 8.3.4.+ に設定するには、次のようなコマンドを発行します。

```
    ibmcloud cf set-env myapp LBP_SERVICE_CONFIG_POSTGRESQL "{driver: { version: 8.3.4.+ }}"
```
{: codeblock}

次の表は、**service_type** と **LBP_SERVICE_CONFIG_xxxx** 環境変数名の対応を示しています。

<table>
<tr>
<th align="left">service_type</th>
<th align="left">環境変数名</th>
</tr>

<tr>
<td>Auto-Scaling</td>
<td>LBP_SERVICE_CONFIG_AUTO-SCALING</td>
</tr>

<tr>
<td>cleardb</td>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
</tr>

<tr>
<td>cloudantNoSQLDB</td>
<td>LBP_SERVICE_CONFIG_CLOUDANTNOSQLDB</td>
</tr>

<tr>
<td>compose-for-mongodb</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MONGO</td>
</tr>

<tr>
<td>compose-for-mysql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
</tr>

<tr>
<td>compose-for-postgresql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
</tr>

<tr>
<td>elephantsql</td>
<td>LBP_SERVICE_CONFIG_POSTGRESQL</td>
</tr>

<tr>
<td>SingleSignOn</td>
<td>LBP_SERVICE_CONFIG_SINGLESIGNON</td>
</tr>
</table>


いくつかのサービス構成オプションをオーバーライドするための構文を、以下の表に示します。

<table>
<tr>
<th align="left">環境変数名</th>
<th align="left">構成の構文</th>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>
</table>



# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
