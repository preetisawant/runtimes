---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 独自の JRE の使用
{: #using_own_jre}

独自の JRE を使用して {{site.data.keyword.Bluemix}} 上で Liberty アプリケーションを実行できます。 liberty-for-java ビルドパックは、[WebSphere Liberty でサポートされているランタイム](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_restrict.html#rwlp_restrict__rest13)のサポートを提供しますが、サポート対象でないバージョンの全機能を保証できるわけではありません。JRE をアプリケーションで使用可能にするには、以下のことを実行する必要があります。
* ビルドパックによるダウンロードが可能なロケーションで JRE をホストする。
* JRE のロケーションが指定されている `index.yml` ファイルをホストする。
* JRE を使用するようにアプリケーションを構成する。

## JRE および `index.yml` のホスト
{: #hosting_jre}

liberty-for-java ビルドパックがダウンロードできる Web サーバーで JRE ファイルをホストする必要があります。このファイルは、使用可能ないずれかのサーバー機能を使用して {{site.data.keyword.Bluemix_notm}} 上でホストすることも、パブリックに使用可能なロケーションでホストすることもできます。 サーバーは、JRE ファイルに関する詳細を指定する `index.yml` ファイルを使用して構成されている必要があります。

JRE および `index.yml` ファイルをホストするには、以下の手順を実行します。
  1. JRE を取得します。これは、UNIX 64 ビット OS で使用するためのバージョンである必要があり、`tar.gz` ファイルでなければなりません。
  2. liberty-for-java ビルドパックがダウンロードできるロケーションで JRE ファイルをホストします。
  3. ホストするロケーションに `index.yml` ファイルを配置します。 `index.yml` ファイルには、JRE のバージョン ID、その後にコロンと JRE ファイルのロケーションの完全な URL が入った項目が含まれている必要があります。
    * `index.yml` ファイルで JRE バージョンを定義します。

    ```
    ---
    jre_version: https://hostingLocation/jreName.tar.gz
    ```
    {: codeblock}

    * JRE バージョン ID と JRE ファイルの完全なロケーションを含めます。  例えば、次のように指定します。

    ```
    ---
    1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```
    {: codeblock}

## アプリケーションの構成
{: #configure_app}

代替の JRE を使用するようにビルドパックを構成するには、Liberty アプリケーションで 2 つの環境変数を設定する必要があります。 `index.yml` ファイルのロケーションを指定するように **JBP_CONFIG_OPENJDK** を設定して、**JVM** 環境変数を *openjdk* に設定します。 version-value ストリングの形式について詳しくは、[『Version Syntax and Ordering and Wildcards』![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/util-repositories.md){: new_window} に関する Cloud Foundry の資料を参照してください。

**JBP_CONFIG_OPENJDK** 変数の値は、`index.yml` ファイルのロケーションと、index.yml ファイルから選択する JRE バージョンです。

```
'{repository_root: "https://locationToIndexYml", version: version-value}'
```
{: codeblock}

`ibmcloud cf se myAPP` コマンドを発行して、**JBP_CONFIG_OPENJDK** 変数を設定します。例えば、次のように指定します。
```
ibmcloud cf se myApp JBP_CONFIG_OPENJDK '{repository_root: "https://myHostingApp.ng.bluemix.net", version: 1.8.+}'
```
{: codeblock}

*repository_root* URL には `index.yml` は含まれていません。 *repository_root* URL は、`index.yml` ファイル自体ではなく、このファイルを含むディレクトリー・レベルを指します。

JVM 環境変数を設定するには、次のコマンドを発行します。
```
ibmcloud cf se myApp JVM 'openjdk'
```
{: codeblock}

**注**: 変更を有効にするには、環境変数の設定後にアプリケーションを再ステージングしてください。

## 確認
{: #confirmation}

Liberty が予期した JRE を使用していることを確認するには、ステージング・ログを調べます。 `index.yml` ファイルに示されているロケーションからサーバーがビルドパックをダウンロードしたことを示すメッセージを検索します。 Liberty が予期した JRE を正常に使用している場合のログ出力の例については、次のスニペットを参照してください。
```
 -----> Downloading OpenJdk 1.8.0_91 from
  https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}
