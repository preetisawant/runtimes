---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# セキュアな Java Web アプリケーションの作成
{: #secure_java_web_app}

Web アプリケーションを設計およびコーディングする際には必ず、重大なセキュリティー脆弱性を取り込むことがないようにセキュリティーを考慮する必要があります。
{: shortdesc}

{{site.data.keyword.Bluemix}} では、セキュアなスターター・アプリケーションが提供されています。これを利用すると、安全性の高い Liberty Java コードを作成でき、ほとんどのクロスサイト・スクリプティング (XSS) 問題を回避できます。 この[セキュアなスターター・アプリケーション](https://github.com/IBM-Cloud/java-secure-app)をダウンロードし、ビルドし、ローカルおよび {{site.data.keyword.Bluemix_notm}} でデプロイすることができます。

## セキュアな Web アプリケーションを作成する理由
{: #why}

セキュリティー脆弱性を突くさまざまなセキュリティー攻撃があります。 攻撃によって、資格情報が盗まれたり、データや機能が失われたり、サービスが破壊されたり、ビジネスの評判や収益が損なわれたりする可能性があります。 クロスサイト・スクリプティング (XSS) は、多くの Web アプリケーションで見られる、回避するべき一般的なセキュリティー脆弱性の 1 つです。

XSS 攻撃の理論や修復技法を学んでから Web アプリケーション開発を始める代わりに、この[セキュアなスターター・アプリケーション](https://github.com/IBM-Cloud/java-secure-app)を使用できます。 このセキュアなスターター・アプリケーションには、XSS を防御するセキュアな主要コーディング手法を示すコーディング例が含まれているため、開発を始めて作業を進めながら XSS 防御技法を学んだり適用したりできます。

## セキュアなサンプル・アプリケーションの使用方法
{: #how}

[セキュアなスターター・アプリケーション](https://github.com/IBM-Cloud/java-secure-app)を、新規 Liberty アプリケーション開発の開始点として使用できます。 まず、このアプリケーションに含まれている XSS 対策コードを理解し、それをアプリケーション API のオペレーションに適用します。 このセキュアなスターター・アプリケーションに含まれている対策は、XSS 攻撃を軽減または防止することによって、サーバーとブラウザーの両方でアプリケーションが悪意のあるユーザー入力によって損傷されるのを防ぐのに役立ちます。

[getting-started-java](https://github.com/IBM-Cloud/get-started-java) サンプル・アプリケーションの場合と同じように、最初にこのセキュアなスターター・アプリケーションをダウンロードしてから、ビルドして {{site.data.keyword.Bluemix_notm}} またはローカルにデプロイします。  {{site.data.keyword.Bluemix_notm}} でのアプリケーションのビルドとデプロイについて詳しくは、[『{{site.data.keyword.Bluemix_notm}} での Liberty 入門』](getting-started.html)を参照してください。  入門として、以下のステップを使用して、アプリケーションの複製、ビルド、および実行を行うことができます。

```
git clone https://github.com/IBM-Cloud/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
http://localhost:9080/GetStartedSecureJava/ でアプリケーションを表示します。

## アプリケーションのすべてのページでの HTTPS の適用
{: #enforce_https}

アプリケーションのすべてのページで HTTP の代わりに HTTPS を適用するには、以下の変更を行う必要があります。

以下のように server.xml を変更して、`appSecurity-2.0` フィーチャーを有効にします。

```
  <featureManager>
    <feature>appSecurity-2.0</feature>
  </featureManager>
```

web.xml ファイルを変更して、以下のセキュリティー制約を組み込みます。

```
  <security-constraint>
    <web-resource-collection>
      <web-resource-name>Entire Application</web-resource-name>
      <url-pattern>/*</url-pattern>
    </web-resource-collection>
    <user-data-constraint>
      <transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
  </security-constraint>
```

これにより、アプリケーションはすべての接続で自動的に HTTPS を使用するように強制し、HTTP 接続を許可しなくなります。

## 詳細情報
{: more}
セキュアなスターター・アプリケーションには **BadServlet.java** が含まれています。 このアプリケーションは、開発者が注意を怠った場合にコーディングする可能性のあるセキュアでないコードの例を示します。

セキュアなスターター・アプリケーションには **GoodServlet.java** も含まれていて、これには多くの優れたセキュアなコーディング手法 (入力の検証、出力のエンコード、セキュアな HTTP ヘッダー設定、Content Security Policy など) が組み込まれています。 これらの手法は、XSS に対する主要な対策です。 これらを適用することによって、他の脆弱性 (インジェクションやディレクトリー・トラバーサルなど) も軽減することができます。

XSS およびその対策について詳しくは、[XSS 防御に関する説明書 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.owasp.org/index.php/XSS){: new_window} を参照してください。
