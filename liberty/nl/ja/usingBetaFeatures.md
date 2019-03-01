---

copyright:
  years: 2015, 2019
lastupdated: "2019-02-01"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ベータ・フィーチャーの使用
{: #using_beta_features}

**重要**:  Liberty for Java ビルドパック v3.28 から、ベータ・ランタイムは含まれないようになりました。  

Liberty ベータ・フィーチャーによって、将来の Liberty リリースに含まれる可能性のある新しい機能およびプログラミング・モデルに早期にアクセスできます。 大部分のベータ・フィーチャーは、{{site.data.keyword.Bluemix}} にデプロイされたアプリケーションでも使用できます。

**重要**: ベータ・フィーチャーは開発およびテスト目的のためにのみ提供され、実動では使用できません。 完全な利用条件については、[ベータのご使用条件](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html)を参照してください。

| フィーチャー |
| ------ |
| `jdbc-4.3` |
| `logstashCollector-1.1` |
| `validator-1.0` |
{: caption="表 1. {{site.data.keyword.Bluemix_notm}} の Liberty for Java で使用可能な Liberty ベータ・フィーチャー" caption-side="top"}

{{site.data.keyword.Bluemix_notm}} で Liberty ベータ・フィーチャーを使用するには、以下を行う必要があります。

1. 以下の例のように、server.xml ファイルで 1 つ以上のベータ・フィーチャーを使用可能にして、[サーバー・ディレクトリーまたはパッケージ化サーバーをデプロイ](/docs/runtimes/liberty/optionsForPushing.html)します。

  ```
<server>
    <featureManager>
        <feature>jdbc-4.3</feature>
    </featureManager>
</server>
  ```
  {: .codeblock}

2.  `IBM_LIBERTY_BETA` 環境変数を `true` に設定します。 この変数は、アプリケーション用にベータ・フィーチャーをインストールして使用可能にするよう Liberty ビルドパックに指示します。  例えば、以下のように指定します。
  * [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/ibmcloud/download_cli.html) を使用します。
    ```
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_BETA true
    ```
    {: .codeblock}

  * あるいは、`manifest.yml` ファイルを使用します。
    ```
      env:
          IBM_LIBERTY_BETA: "true"
    ```
    {: .codeblock}

3. `JBP_CONFIG_LIBERTY` 環境変数を `"version: +"` に設定します。 この変数は、ベータ・フィーチャーをサポートする [Liberty 月次ランタイム](/docs/runtimes/liberty/buildpackDefaults.html#liberty_versions)を使用可能にします。 例えば、以下のように指定します。
  * {{site.data.keyword.Bluemix_notm}} CLI ツールを使用します。
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ```
    {: .codeblock}

  * あるいは、`manifest.yml` ファイルを使用します。
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
    ```
    {: .codeblock}

既存のアプリケーションでベータ・フィーチャーを使用可能にする場合は、環境変数を設定した後でアプリケーションを再ステージングすることを忘れないでください。
