---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Cloud Runtime for Swift
{: #swift_runtime}

{{site.data.keyword.Bluemix}} 上の Runtime for Swift は、[{{site.data.keyword.Bluemix_notm}} buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack) (つまり swift_buildpack) を採用しています。
このビルドパックは、Swift アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} は、Kitura ベースの Swift [スターター・アプリケーション ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Cloud/Kitura-Starter)を提供します。 Kitura スターター・アプリケーションは、Swift プログラミング言語を使用して開発可能なサーバー・アプリケーションのタイプを確認するために使用できる、シンプルな Swift アプリケーションです。 このサンプル・アプリケーションは、HTML コンテンツをクライアントに返す、基本的な Kitura HTTP サーバーを作成します。

**注:** Kitura スターター・アプリケーションは、教育目的での使用を意図しています。 機能拡張を行ってスターター・アプリケーションを試し、これらの変更を {{site.data.keyword.Bluemix_notm}} 環境に対してプッシュすることができます。 スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](../common/starter_app_usage.html)を参照してください。

## アプリケーションの名前変更
{: #renaming_your_app}

Kitura スターターから、またはより一般的な方法で、アプリケーションの名前を変更する場合は、対処する必要のある変更がいくつかあります。 これによって混乱を避けることができ、さらに確実にエラーのないデプロイメントを実現できます。

- アプリケーションのプロジェクト・フォルダーの名前を、アプリケーションの名前と一致するように変更します。
- `Package.swift` - 次のエントリーを変更します。
    - `name` - アプリケーションの名前と一致している必要があります。
    - `targets[Target(name:)]` - アプリケーションの名前と一致している必要があります。
- `manifest.yml` - 次のエントリーを変更します。
    - `name` - アプリケーションの名前と一致している必要があります。
    - `command` - アプリケーションを開始する実行可能ファイルの名前 (Package.swift ファイルに指定した名前と一致している必要があります)。

## ランタイム・バージョン
{: #runtime_versions}

{{site.data.keyword.Bluemix_notm}} 上でホストされる [Runtime for Swift ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Swift/swift-buildpack) (swift_buildpack) は、最新の GA バージョンの Swift バイナリーを使用するように更新されています。 これは、アプリケーションで使用する Swift の推奨されるバージョンです。 ビルドパックは、その [manifest.yml ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) ファイル内に他の Swift バージョンをリストします。これらのバージョンは、プロビジョニング時間を短縮するためにビルドパックにキャッシュされます。

アプリケーション用に {{site.data.keyword.Bluemix_notm}} 上で別のバージョンの Swift を使用する場合は、リポジトリーのルートにある `.swift-version` ファイルを使用して、バージョンを指定できます。 この `.swift-version` ファイルは、swift_buildpack によって使用される Swift バージョンを定義します。

```
$ cat .swift-version
4.1.2
```
{: pre}

Swift 言語は頻繁に更新されるため、連携して動くことがわかっている Swift バージョンにアプリケーションが「ピン留め」されるように、常に `.swift-version` ファイルを組み込む必要があります。

有効であればどのバージョンの Swift でも `.swift-version` ファイル内に指定できることに注意してください。 これらの代替バージョンは、[Swift.org ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://swift.org/download/) の命名と一致する必要があり、Swift.org から直接ダウンロードされます。 非キャッシュ・バージョンを使用するとプロビジョンに少し時間がかかりますが、Swift アプリケーションのランタイム・パフォーマンスに相違はありません。

{{site.data.keyword.Bluemix_notm}} のデフォルトの swift_buildpack は、アプリケーションのルート・ディレクトリーに `Package.swift` ファイルが含まれている場合に使用されます。  代替のビルドパックを使用する場合は、`buildpack: {buildpackUrl}` エントリーをアプリケーションの manifest.yml ファイルに追加することでこれを指定する必要があります。 または、デプロイメント時に `ibmcloud cf push -b {buildpackUrl}` コマンド引数を使用してこれを定義することができます。


## 開発者環境

開発者には、Swift を使用してサーバー・サイド・アプリケーションを作成するときにいくつかのオプションがあります。 Apple macOS デバイスを使用する場合は、Xcode IDE の使用をお勧めしますが、これは要件ではありません。  {{site.data.keyword.Bluemix_notm}} でデプロイおよび実行される Swift ベースのアプリケーションは、任意のプログラミング編集機能や IDE を使用できます。  多くの一般的な編集機能では、Swift の構文の強調表示と lint 機能を使用できます。 [Swift.org ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://swift.org/) のバイナリーに組み込まれている Swift REPL コマンド・ライン・ツールを使用すると、{{site.data.keyword.Bluemix_notm}} にデプロイする前に、ローカルでコンパイルとテストを行うことができます。

macOS ユーザーの場合は、{{site.data.keyword.Bluemix_notm}} で実行されるサーバー・サイドの Swift アプリケーションの作成、デプロイメント、管理、および制御を単純化する [Kitura App ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.kitura.io/app.html) を使用することができます。  


## 統合の拡張

[Kitura Web フレームワーク](http://ibm-swift.github.io/Kitura/)との連携により、多数の機能が提供されます。 Kitura は実際にはモジュラーであるため、認証、Watson ベースのサービスへのアクセス、さまざまなデータベースなどのフィーチャーを提供するために、パッケージされた SDK を使用してすぐにその機能を拡張する必要が生じます。  Kitura は多数のデータベースのサポートを直接提供しますが、その他のオープン・ソースのプロジェクトも多くのデータベース・プラットフォーム用の SDK を提供しています。 Kitura で提供され、外部リソースを処理する SDK の一部を以下にリストします。

- [IBM Watson Developer Cloud Swift SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/watson-developer-cloud/swift-sdk/)
- [SwiftMetrics ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/RuntimeTools/SwiftMetrics)
- [IBM Cloudant および CouchDB ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Swift/Kitura-CouchDB)
- [KituraKit ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Swift/KituraKit)
- [Swift Kuery ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Swift/Swift-Kuery/)
- [Swift Kuery ORM ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Swift/Swift-Kuery-ORM)

アプリケーションに含める他の Swift パッケージを見つけるには、[Kitura.io](https://www.kitura.io/packages.html)の「パッケージ」セクションに進んでください。 パッケージは、パッケージの Git URL とバージョンの詳細をアプリケーションの `Package.swift` ファイルに含めることで Swift アプリケーションに追加することができます。 パッケージ管理の詳細については、[Swift.org の『Package Manager』セクション](https://swift.org/package-manager/)を参照してください。


## 関連情報

Swift 開発者用のその他のオンライン・ツールも IBM から入手できます。
- [IBM Swift DevCenter ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/swift/) - すべての IBM Swift 情報の主なランディング・サイト。 オファリング、ブログ、ソーシャル・イベント、資料などに関する情報を見つけることができます。
- [Kitura.io ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.kitura.io/index.html) は、Kitura アプリケーションをビルドするためのニュース、サンプル、およびリソースを提供します。
- [Swift@IBM Slack ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://swift-at-ibm-slack.mybluemix.net/) は、Swift@IBM チームに質問をし、Swift@IBM チームと一緒に問題を解決するためのフォーラムを提供します。
