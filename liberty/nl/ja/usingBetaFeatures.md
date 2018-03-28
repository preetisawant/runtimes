---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ベータ・フィーチャーの使用
{: #using_beta_features}

Liberty ベータ・フィーチャーによって、将来の Liberty リリースに含まれる可能性のある新しい機能およびプログラミング・モデルに早期にアクセスできます。 大部分のベータ・フィーチャーは、{{site.data.keyword.Bluemix}} にデプロイされたアプリケーションでも使用できます。

**重要**: ベータ・フィーチャーは開発およびテスト目的のためにのみ提供され、実動での使用には向いていない場合があります。 完全な利用条件については、[ベータのご使用条件](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html)を参照してください。

{{site.data.keyword.Bluemix_notm}} で使用可能な Liberty ベータ・フィーチャー
<table>
<tr>
<th align="left">フィーチャー</th>
</tr>

<tr>
    <tr><td>appSecurity-3.0</tr></td>
    <tr><td>audit-1.0</tr></td>
    <tr><td>beanValidation-2.0</tr></td>
    <tr><td>bluemixLogCollector-1.1</tr></td>
    <tr><td>cdi-2.0</tr></td>
    <tr><td>javaee-8.0</tr></td>
    <tr><td>javaeeClient-8.0</tr></td>
    <tr><td>jaxrs-2.1</tr></td>
    <tr><td>jpa-2.2</tr></td>
    <tr><td>jpaContainer-2.2</tr></td>
    <tr><td>jsf-2.3</tr></td>
    <tr><td>jsfContainer-2.2</tr></td>
    <tr><td>jsonb-1.0</tr></td>
    <tr><td>jsonbContainer-1.0</tr></td>
    <tr><td>jsonp-1.1</tr></td>
    <tr><td>jsonpContainer-1.1</tr></td>
    <tr><td>logstashCollector-1.1</tr></td>
    <tr><td>mpConfig-1.2</tr></td>
    <tr><td>mpOpenAPI-1.0</tr></td>
    <tr><td>mpRestClient-1.0</tr></td>
    <tr><td>opentracing-1.0</tr></td>
    <tr><td>servlet-4.0</tr></td>
    <tr><td>validator-1.0</tr></td>
    <tr><td>webProfile-8.0</tr></td>

</tr>
</table>

{{site.data.keyword.Bluemix_notm}} で Liberty ベータ・フィーチャーを使用するには、以下を行う必要があります。

1. 以下の例のように、server.xml ファイルで 1 つ以上のベータ・フィーチャーを使用可能にして、[サーバー・ディレクトリーまたはパッケージ化サーバーをデプロイ](optionsForPushing.html)します。
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>mpOpenAPI-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  **IBM_LIBERTY_BETA** 環境変数を **true** に設定します。 この変数は、アプリケーション用にベータ・フィーチャーをインストールして使用可能にするよう Liberty ビルドパックに指示します。  例えば、以下のように指定します。
  * cf コマンド・ライン・ツールを使用する場合
```
       $ cf set-env <yourappname> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * manifest.yml ファイルを使用する場合
```
      env:
          IBM_LIBERTY_BETA: "true"
```

3. **JBP_CONFIG_LIBERTY** 環境変数を **"version: +"** に設定します。 この変数は、ベータ・フィーチャーをサポートする [Liberty 月次ランタイム](buildpackDefaults.html#liberty_versions)を使用可能にします。 例えば、以下のように指定します。
  * cf コマンド・ライン・ツールを使用する場合
```
       $ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * manifest.yml ファイルを使用する場合
```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
```

既存のアプリケーションでベータ・フィーチャーを使用可能にする場合は、環境変数を設定した後でアプリケーションを再ステージングすることを忘れないでください。

{: #codeblock}

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Liberty for Java ランタイム](index.html)
* [Liberty の概要](https://www.ibm.com/support/knowledgecenter/SSAW57_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/cwlp_about.html)
