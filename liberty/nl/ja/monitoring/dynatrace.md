---

copyright:
  years: 2016, 2018
lastupdated: "2018-06-27"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dynatrace を使用した {{site.data.keyword.cloud_notm}} 内の Liberty のモニター
{: #using_dynatrace}

Dynatrace は、アプリケーションのモニタリングを提供するサード・パーティー・サービスです。 Dynatrace を Liberty アプリケーションに統合することは可能ですが、IBM はサード・パーティー・サービスに関するサポートは提供しません。 詳しくは、[サード・パーティー・サービス](/docs/runtimes-common/buildpackSupport.html#third-party)を参照してください。

Dynatrace とそのライセンスについて詳しくは、[Dynatrace の『Application Monitoring』 ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.dynatrace.com/en/products/application-monitoring.html) を参照してください。

Liberty アプリケーションが Dynatrace を使用するように構成されている場合、デフォルトの動作では、Liberty ランタイムは Dynatrace サイトから Dynatrace エージェント `.jar` ファイルを取得し、その Dynatrace エージェントをアプリケーションで実行します。  このデフォルトの動作では、Dynatrace を使用するために必要な最小構成は、Dynatrace コレクターを指すユーザー提供のサービスを作成することです。

## Dynatrace コレクターを指すユーザー提供のサービスの作成

まず、Dynatrace コレクターをセットアップする必要があります。  次に、Dynatrace エージェントが Dynatrace コレクターと接続するための情報を渡す、ユーザー提供のサービスを作成する必要があります。 Dynatrace コンポーネント間の関係について詳しくは、[Dynatrace の『Architecture』 ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://community.dynatrace.com/community/display/DOCDT65/Architecture) を参照してください。

1. Dynatrace コレクターをセットアップします。
  * Dynatrace コレクターのダウンロード手順およびセットアップ手順については、[Dynatrace コミュニティーの Web サイト ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace) を参照してください。
  * コレクターは、{{site.data.keyword.Bluemix_notm}} 内のアプリケーションで実行されている Dynatrace エージェントにアクセス可能なロケーションでセットアップするようにしてください。
2. 実行中の Dynatrace コレクターを指すユーザー提供サービスを作成します。

  **注:** ユーザー提供サービスの名前には **dynatrace** という文字列が含まれている必要があります。 大/小文字は無視されます。 例えば次のコマンドを使用します。この例の **my-dynatrace-collector** には **dynatrace** が含まれています。
  ```
  ibmcloud cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
  ```
  {: codeblock}

    この例では、my-dynatrace-collector はサービスに付けられた名前、DynatraceCollectorIPaddress は構成済み Dynatrace コレクターの IP アドレス、profile はこのモニター対象アプリケーションに関連付けられたオプションの Dynatrace プロファイル名です。 デフォルト・プロファイル値は Monitoring です。 オプション・パラメーターは次の例のように指定できます。

    ```
    ibmcloud cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                      "options" : {"dynatrace-parameter-1": "value",
                                   "dynatrace-parameter-2": "value"}}'
    ```
    {: codeblock}

    使用可能なオプションについて詳しくは、Dynatrace コミュニティー Web サイトの[『Agent Configuration』の『_Agent Settings_』セクション ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://community.dynatrace.com/community/display/DOCDT65/Set+up+Agents) を参照してください。 例えば、exclude オプションを使用すると、Dynatrace のモニター対象からクラスを除外できます。 ユーザー提供サービスの構成について詳しくは、[『Dynatrace Agent Framework』 ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md) を参照してください。

3. アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュした後で、作成したユーザー提供サービスをアプリケーションにバインドします。 例えば、次のコマンドを使用します。
  ```
  ibmcloud cf bs myApp my-dynatrace-collector
  ```
  {: codeblock}

    **注:** サービスのバインド後にアプリケーションを再ステージングする必要があります。

## オプション構成
{: #optional_configuration}

ユーザー自身が Dynatrace エージェント `.jar` ファイルを取得し、ホストすることも可能です。  その場合は、以下の追加の構成ステップが必要です。
1. Liberty ビルドパックでダウンロードできるように、Dynatrace エージェント `.jar` ファイルを獲得し、ホストします。
2. Dynatrace エージェントをダウンロードできるように、Liberty アプリケーションを構成します。

### Dynatrace エージェントのホスティング
{: #hosting_dynatrace_agent}
Dynatrace エージェントは Web サーバー上でホストされる必要があり、Liberty ビルドパックはそのサーバーからエージェント `.jar` ファイルをダウンロード可能でなければなりません。 サーバーは、エージェント `.jar` ファイルに関する詳細を指定する `index.yml` ファイルを使用して構成されている必要があります。 Dynatrace エージェントをセットアップするには、以下の手順に従ってください。
  1. Dynatrace エージェント `.jar` ファイルをダウンロードします。 Dynatrace エージェント `.jar` ファイルのダウンロード手順については、Dynatrace コミュニティー Web サイトの[『Dynatrace Server Platform Installers』 ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace) を参照してください。 {{site.data.keyword.Bluemix_notm}} 上で実行するための適切なエージェント `.jar` ファイルは、**dynatrace-agent-unix.jar** バージョン **6.+** です。
  2. Liberty ビルドパックによるダウンロードが可能なロケーションでエージェント `.jar` ファイルをホストします。 このファイルは、使用可能ないずれかのサーバー機能を使用して {{site.data.keyword.Bluemix_notm}} 自体の上でホストすることも、パブリックに使用可能なロケーションでホストすることもできます。
     * ホストするロケーションに必ず `index.yml` ファイルを配置します。 `index.yml` ファイルには、エージェント `.jar` ファイルのバージョン ID その直後のコロン、およびエージェント `.jar` ファイルのロケーションの完全な URL からなる項目が含まれていなければなりません。 例えば、次のとおりです。

            ---
               6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
            {: codeblock}

     * **dynatrace-agent-6.3.0-unix.jar** ファイルは、`index.yml` ファイル内に指定されたロケーションで使用可能でなければなりません。 `.jar` ファイルと `index.yml` の両方のロケーションを同じディレクトリーにすることができます。

### Liberty アプリケーションの構成
{: #configuring_liberty_app}

モニター対象の Liberty アプリケーションは、以前にセットアップしたエージェント `.jar` ファイルをホストするサーバーを検出するように構成する必要があります。 アプリケーションの構成に **JBP_CONFIG_DYNATRACEAPPMONAGENT** 環境変数を使用できます。 **JBP_CONFIG_DYNATRACEAPPMONAGENT** 環境変数は、ビルドパックに Dynatrace エージェントをどこからダウンロードするかを示します。 この環境変数を設定するには、以下の手順に従ってください。

1. 値が *「repository_root: URL_of_server_hosting_index.yml」* になるように変数 **JBP_CONFIG_DYNATRACEAPPMONAGENT** を設定します。 例えば、アプリケーションのプッシュ後に次のコマンドを発行します。

        ibmcloud cf se myApp JBP_CONFIG_DYNATRACEAPPMONAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
        {: codeblock}

    この例では、*my-dynatrace-agent-host.mybluemix.net* は、以前に構成したサーバーでホストされる `index.yml` ファイルの URL です。

2. 環境変数の設定後、アプリケーションを再ステージングします。 ステージング・ログを調べて、エージェントをホストするサーバーからの Dynatrace エージェントのダウンロードが成功したことを示すメッセージがあることを確認してください。 例えば、次のとおりです。
```
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
```
{: codeblock}
