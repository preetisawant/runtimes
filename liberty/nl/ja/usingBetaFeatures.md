---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-03"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ベータ・フィーチャーの使用
{: #using_beta_features}

Liberty ベータ・フィーチャーによって、将来の Liberty リリースに含まれる可能性のある新しい機能およびプログラミング・モデルに早期にアクセスできます。 大部分のベータ・フィーチャーは、{{site.data.keyword.Bluemix}} にデプロイされたアプリケーションでも使用できます。

**重要**: ベータ・フィーチャーは開発およびテスト目的のためにのみ提供され、実動では使用できません。完全な利用条件については、[ベータのご使用条件](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html)を参照してください。

| フィーチャー |
| ------ |
| `appSecurity-3.0` |
| `audit-1.0` |
| `beanValidation-2.0` |
| `cdi-2.0` |
| `javaee-8.0` |
| `javaeeClient-8.0` |
| `jaxrs-2.1` |
| `jpa-2.2` |
| `jpaContainer-2.2` |
| `jsf-2.3` |
| `jsfContainer-2.3` |
| `jsonb-1.0` |
| `jsonbContainer-1.0` |
| `jsonp-1.1` |
| `jsonpContainer-1.1` |
| `logstashCollector-1.1` |
| `servlet-4.0` |
| `usageMetering-1.0` |
| `validator-1.0` |
| `webProfile-8.0` |
{: caption="表 1. {{site.data.keyword.Bluemix_notm}} の Liberty for Java で使用可能な Liberty ベータ・フィーチャー" caption-side="top"}

{{site.data.keyword.Bluemix_notm}} で Liberty ベータ・フィーチャーを使用するには、以下を行う必要があります。

1. 以下の例のように、server.xml ファイルで 1 つ以上のベータ・フィーチャーを使用可能にして、[サーバー・ディレクトリーまたはパッケージ化サーバーをデプロイ](optionsForPushing.html)します。

  ```
<server>
    <featureManager>
        <feature>servlet-4.0</feature>
        <feature>webProfile-8.0</feature>
    </featureManager>
</server>
  ```
  {: .codeblock}

2.  `IBM_LIBERTY_BETA` 環境変数を `true` に設定します。 この変数は、アプリケーション用にベータ・フィーチャーをインストールして使用可能にするよう Liberty ビルドパックに指示します。  例えば、以下のように指定します。
  * [{{site.data.keyword.Bluemix_notm}} CLI (../../cli/reference/bluemix_cli/download_cli.html) を使用します。
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

3. `JBP_CONFIG_LIBERTY` 環境変数を `"version: +"` に設定します。 この変数は、ベータ・フィーチャーをサポートする [Liberty 月次ランタイム](buildpackDefaults.html#liberty_versions)を使用可能にします。 例えば、以下のように指定します。
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
