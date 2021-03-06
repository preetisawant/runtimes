---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-24"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# SDK for Node.js ビルドパックに対する最新の更新
{: #latest_updates}

sdk-for-nodejs ビルドパックの最新更新のリスト。

## 2018 年 7 月 24 日: 更新された Node.js ビルドパック v3.21
{:#fips-deprecation}
**重要:** このリリースの最新の Node.js 6.x および 8.x のバージョンから、SDK for Node.js ビルドパックは、Node.js コミュニティー・リリースに基づきます。この変更により、ビルドパック内の Node.js OpenSSL FIPS モジュールは更新されなくなります。現在の OpenSSL FIPS モジュールおよび IBM SDK for Node.js ビルドは、2018 年 8 月 24 日現在、削除の対象です。詳しくは、[Aligning the Node.js Buildpack to Community Runtimes (Node.js ビルドパックをコミュニティー・ランタイムに合わせる)![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://admin.blogs.prd.ibm.event.ibm.com/blogs/bluemix/?p=139660)ブログ投稿を参照してください。

SDK for Node.js ビルドパック v3.21 では、IBM SDK for Node.js バージョン 4.8.5、4.8.7、6.13.0、8.9.4、および Node.js コミュニティーのバージョン 6.14.3、8.11.3 が提供されます。デフォルトは最新の 6.x です。したがって、現在は 6.14.3 です。

このリリースには、以下のセキュリティー脆弱性に対する修正も含まれます。
* [CVE-2018-0739](http://www.ibm.com/support/docview.wss?uid=swg22016251)

## 2018 年 6 月 1 日: 更新された Node.js ビルドパック v3.20.2
SDK for Node.js ビルドパック v3.20.2 では、現行の Node.js ランタイムに対する Dynatrace Managed PaaS 統合が追加されます。 『[Dynatrace を使用した {{site.data.keyword.cloud_notm}} 内の Node.js のモニター](dynatrace.html)』を参照してください。

## 2018 年 5 月 17 日: 更新された Node.js ビルドパック v3.20.1
SDK for Node.js ビルドパック v3.20.1 では、現行の Node.js ランタイムに対する Dynatrace PaaS 統合が修正されます。 『[Dynatrace を使用した {{site.data.keyword.cloud_notm}} 内の Node.js のモニター](dynatrace.html)』を参照してください。

## 2018 年 4 月 9 日: 更新された Node.js ビルドパック v3.20
SDK for Node.js ビルドパック v3.20 では、現行の Node.js ランタイムに対する Dynatrace PaaS 統合が追加されます。 『[Dynatrace を使用した {{site.data.keyword.cloud_notm}} 内の Node.js のモニター](dynatrace.html)』を参照してください。

## 2018 年 3 月 16 日: 更新された Node.js ビルドパック v3.19
SDK for Node.js ビルドパック v3.19 では、IBM SDK for Node.js バージョン 4.8.5、4.8.7、6.12.3、6.13.0、8.9.3、および 8.9.4 が提供されます。 デフォルトは最新の 6.x です。したがって、現在は 6.13.0 です。

## 2018 年 2 月 6 日: 更新された Node.js ビルドパック v3.18
SDK for Node.js ビルドパック v3.18 では、IBM SDK for Node.js バージョン 4.8.5、4.8.7、6.12.2、6.12.3、8.9.3、および 8.9.4 が提供されます。 デフォルトは最新の 6.x です。したがって、現在は 6.12.3 です。

## 2018 年 1 月 8 日: 更新された Node.js ビルドパック v3.17
SDK for Node.js ビルドパック v3.17 では、IBM SDK for Node.js バージョン 4.8.5、4.8.7、6.12.0、6.12.2、8.9.0、および 8.9.3 が提供されます。 デフォルトは最新の 6.x です。したがって、現在は 6.12.2 です。

## 2017 年 12 月 11 日: 更新された Node.js ビルドパック v3.16.1
SDK for Node.js ビルドパック v3.16.1 では、IBM SDK for Node.js バージョン v4.8.4、v4.8.5、v6.11.4、v6.12.0、v8.6.0、v8.9.0 が提供されます。 デフォルトは最新の 6.x です。従って、現在は 6.12.0 です。
これは、「アドバイザリー ID: 10237 製品レコード ID: 104487 タイトル: Node.js zlib DOS セキュリティーの脆弱性、2017 年 10 月」(CVE-2017-14919) の PSIRT を修正します。 8.6.0.0 以前、6.10.2.0 から 6.11.4.0、および 4.8.2.0 から 4.8.4.0 に影響するセキュリティー脆弱性に対する修正を取り入れるために、v3.16.1 にアップグレードすることをお勧めします。

## 2017 年 11 月 1 日: 更新された Node.js ビルドパック v3.15
SDK for Node.js ビルドパック v3.15 では、IBM SDK for Node.js バージョン 4.8.3、4.8.4、6.11.3、6.11.4、8.3.0、および 8.6.0 が提供されます。 デフォルトは最新の 6.x です。従って、現在は 6.11.4 です。

## 2017 年 9 月 20 日: 更新された Node.js ビルドパック v3.14
SDK for Node.js ビルドパック v3.14 では、IBM SDK for Node.js バージョン 4.8.3、4.8.4、6.11.2、6.11.3、8.1.4、および 8.3.0 が提供されます。 デフォルトは最新の 6.x です。従って、現在は 6.11.3 です。 このリリースでは、Node.js アプリケーションを[安全にシャットダウン](https://docs.cloudfoundry.org/devguide/deploy-apps/app-lifecycle.html#shutdown)できないようにしていたビルドパックのバグが修正されました。

## 2017 年 7 月 26 日: 更新された Node.js ビルドパック v3.13
SDK for Node.js ビルドパック v3.13 では、IBM SDK for Node.js バージョン 4.8.3、4.8.4、6.11.0、6.11.1、8.1.2、および 8.1.4 が提供されます。 デフォルトは最新の 6.x です。したがって、現在は 6.11.1 です。 バージョン 8 はテスト用に使用可能ですが、実動用にはまだ推奨されていません。  

このビルドパックには、Node.js で検出された最近のセキュリティー脆弱性に対処する、更新された Node.js バージョンが含まれています。 ユーザーは、入手可能な最新バージョンを使用するようにアプリケーションを更新した後、{{site.data.keyword.Bluemix_notm}} 内でアプリケーションを再ステージングする必要があります。  Node.js のセキュリティー脆弱性に対する修正 CVE-2017-1000381 および CVE-2017-11499 について詳しくは、<a href="http://www-01.ibm.com/support/docview.wss?uid=swg22006722">このセキュリティー情報</a>を参照してください。

## 2017 年 5 月 5 日: 更新された Node.js ビルドパック v3.12
SDK for Node.js ビルドパック v3.12 では、IBM SDK for Node.js バージョン 0.12.17、0.12.18、4.8.0、4.8.2、6.10.0、および 6.10.2 が提供されます。 デフォルトは最新の 4.x から最新の 6.x に変更されました。したがって、現在は 6.10.2 です。 これは、メジャー・バージョンの変更であるため、デフォルトに依存するアプリケーションに影響を及ぼす可能性があります。 問題を回避する方法について詳しくは、[Node.js version long-term support and the SDK for Node.js buildpack](https://www.ibm.com/blogs/bluemix/2016/11/node-version-support-and-sdk-buildpack/) を参照してください。

新規ランタイムに加えて、このリリースには、アプリケーション管理ヘルス・センター・ハンドラーおよび Node.js バージョン 6.9.5 と 6.10.0 に関する問題のビルドパック・バグ修正も含まれています。

## 2017 年 3 月 10 日: 更新された Node.js ビルドパック v3.11
このリリースのビルドパックは、IBM SDK for Node.js ランタイムのバージョン 0.10.47、0.10.48、0.12.17、0.12.18、4.7.3、4.8.0、6.9.5、および 6.10.0 をサポートします。 現在のデフォルトのバージョンは 4.8.0 です。

新規ランタイムに加えて、このリリースには、devconsole UI を使用してシェル・アプリケーション管理ハンドラーを有効化したときに起こるバグの修正も含まれています。 このビルドパックでは、Monitoring and Analytics サービスに対する自動構成の処理も変更されました。 無料プランを使用するアプリケーションにはログ機能が追加されなくなり、この機能は logmet で置き換えられます。

## 2017 年 1 月 20 日: 更新された Node.js ビルドパック v3.10
このリリースのビルドパックは、IBM SDK for Node.js ランタイムのバージョン 0.10.47、0.10.48、0.12.17、0.12.18、4.7.0、4.7.2、6.9.2、および 6.9.4 をサポートします。 現在のデフォルトは 4.7.2 です。  このリリースは、[Cloud Foundry Node.js ビルドパック v1.5.24](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.24) とも同期しています。
アプリケーションの開始のために必ずしも「npm start」が呼び出されるとは限らないというバグの修正が含まれています。

## 2016 年 11 月 17 日: 更新された Node.js ビルドパック v3.9
このリリースのビルドパックは、IBM SDK for Node.js ランタイムのバージョン 0.10.47、0.10.48、0.12.16、0.12.17、4.6.1、4.6.2、6.7.0、および 6.9.1 をサポートします。 現在のデフォルトは 4.6.2 です。

Node.js v6 は 2016 年 10 月 18 日に LTS ステータスにプロモートされ、まもなくビルドパックのデフォルトのランタイムになることに注意してください。 Node.js v0.10 の存続期間は 2016 年 10 月 31 日に終わりに達したため、まもなくビルドパックに含まれなくなります。 詳しくは、[Node.js version long-term support and the SDK for Node.js buildpack](https://www.ibm.com/blogs/bluemix/2016/11/node-version-support-and-sdk-buildpack/) を参照してください。

Node.js v6 と組み合わせて使用されたときにアプリケーション管理ハンドラーのトレースおよびインスペクターに影響するバグがこのリリースで対処されました。 Node.js v6 がインスペクター機能を統合したことをインスペクター・ハンドラーがどのように変更するのかについて詳しくは、『[Liberty および Node.js アプリケーションの管理](../common/app_mng.html#inspector)』を参照してください。

## 2016 年 10 月 7 日: Node.js ビルドパック v3.8-20161006-1211 の更新
このリリースのビルドパックは、IBM SDK for Node.js ランタイムのバージョン 0.10.46、0.10.47、0.12.15、0.12.16、4.5.0、4.6.0、6.6.0、および 6.7.0 をサポートします。 現在のデフォルトは 4.6.0 です。

新規ランタイムに加えて、このリリースにはビルドパックのバグ修正も含まれています。 v3.7-20160826-1101 リリース更新で言及された Node.js 6.x と開発モードの使用時の既知の問題の修正がその 1 つです。 このリリースは、[Cloud Foundry Node.js ビルドパック v1.5.20](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.20) とも同期しています。

## 2016 年 8 月 26 日: 更新された Node.js ビルドパック v3.7-20160826-1101
このリリースのビルドパックは、IBM SDK for Node.js ランタイムのバージョン 0.10.45、0.10.46、0.12.14、0.12.15、4.4.7、4.5.0、6.2.2、および 6.4.0 をサポートします。 現在のデフォルトは 4.5.0 です。

このリリースは、[Cloud Foundry の Node.js ビルドパック 1.5.18](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.18) からのものを含むバグ修正を組み込みます。

このリリースは、[{{site.data.keyword.Bluemix_notm}}『Node.js Buildpack v3.3 – FIPS mode and more』](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/)で発表されたように、strongpm アプリケーション管理ハンドラーのサポートを削除します。

Node.js 6.x および[開発モード](../common/app_mng.html#devmode)の使用時には既知の問題があることに注意してください。 回避策として、開発モードを有効にした後で、使用を開始する前にアプリケーションを再ステージする必要があります。

## 2016 年 7 月 22 日: 更新された Node.js ビルドパック v3.6-20160715-0749
このリリースのビルドパックは、IBM SDK for Node.js ランタイムのバージョン 0.10.45、0.10.46、0.12.14、0.12.15、4.4.6、4.4.7、6.2.1、および 6.2.2 をサポートします。 現在のデフォルトは 4.4.7 です。

このリリースには、フェデレーテッド・ログインをサポートする、更新されたアプリケーション管理プロキシーが含まれています。

以下のセキュリティー脆弱性に関する修正が組み込まれました。
* [CVE-2016-1669](http://www-01.ibm.com/support/docview.wss?uid=swg21986383)

## 2016 年 6 月 22 日: 更新された Node.js ビルドパック v3.5-20160609-1608

このリリースのビルドパックは、IBM SDK for Node.js ランタイムのバージョン 4.4.5 および 6.2.0 を追加します。 デフォルトは 4.4.5 になります。

このリリースは、[{{site.data.keyword.Bluemix_notm}}『Node.js Buildpack v3.3 – FIPS mode and more』](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/)で発表されたように、古いランタイム・バージョンのサポートを削除します。 ビルドパックは現在、0.10.44、0.10.45、0.12.13、0.12.14、4.4.4、4.4.5、6.1.0、および 6.2.0 をサポートします。

このリリースは、[Cloud Foundry の Node.js ビルドパック 1.5.14](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.14) からバグ修正を組み込みます。

## 2016 年 5 月 20 日: 更新された Node.js ビルドパック v3.4-20160518-1653

このリリースのビルドパックは、IBM SDK for Node.js ランタイムのバージョン 0.10.45、0.12.14、4.4.4、6.0.0、および 6.1.0 を追加します。 現在のデフォルトは 4.4.4 です。

以下のセキュリティー脆弱性に関する修正が組み込まれました。
* [CVE-2015-8855](http://www-01.ibm.com/support/docview.wss?uid=swg21982852)
* [CVE-2016-2108 CVE-2016-2107 CVE-2016-2105 CVE-2016-2106 CVE-2016-2109 CVE-2016-2176 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.openssl.org/news/secadv/20160503.txt)

npm v3 およびアプリケーション管理インスペクター・ユーティリティーに関する既知の問題があります。 npm 3.8.6 は、6.0.0 ランタイムおよび 6.1.0 ランタイムでのデフォルトです。 いずれかの 6.x ランタイムおよびインスペクター・ユーティリティーを使用する場合、一時的な回避策として、package.json に 2.x npm バージョンを指定する必要があります。

## 2016 年 4 月 29 日: 更新された Node.js ビルドパック v3.3-20160428-1409

このリリースのビルドパックは、IBM SDK for Node.js ランタイムのバージョン 0.10.44、0.12.13、4.4.0、4.4.1、4.4.2、および 4.4.3 を追加します。 デフォルトは現在、4.4.3 です。
バージョン 4.3.1 以降では、アプリケーションに対して `FIPS_MODE=true` 環境変数を設定することにより、FIPS 対応バージョンのランタイムを使用できるようになりました。

更新されたビルドパックと新しいランタイム・バージョンにも、以下のセキュリティー脆弱性に対する修正が含まれています。
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

更新されたビルドパックには、以下のように、いくつかのバグの修正も含まれています。
* 要求される範囲に一致する IBM SDK for Node.js ビルドが使用できる場合、そのビルドが常に使用されるようになりました。 以前は、このケースに該当するのは 4.x ランタイム・バージョンのみでした。
* アプリケーション管理インスペクター・ユーティリティーが 4.x ランタイム・バージョンで機能するようになりました。
* strongpm アプリケーション管理ユーティリティーの不具合が修正されました。

## 2016 年 3 月 18 日: 更新された Node.js ビルドパック v3.2-20160315-1257

このリリースのビルドパックは、デフォルトの IBM SDK for Node.js ランタイムをバージョン 4.3.0 から 4.3.2 へ移行します。 このビルドパックには、IBM SDK for Node.js バージョン 0.10.43、0.12.12、および 4.3.1 も含まれています。 いくつかのセキュリティー脆弱性に対する修正を適用するには、これらの新しい Node.js バージョンを使用します。

## 2016 年 3 月 4 日: 更新された Node.js ビルドパック v3.1-20160222-1123

このリリースのビルドパックは、デフォルトの IBM SDK for Node.js ランタイムをバージョン 4.2.4 から 4.3.0 へ移行します。 このビルドパックには、IBM SDK for Node.js バージョン 0.10.42、0.12.10、および 4.2.6 も含まれています。 いくつかのセキュリティー脆弱性に対する修正を適用するには、これらの新しい Node.js バージョンを使用します。

## 2016 年 2 月 4 日: 更新された Node.js ビルドパック v3.0-20160125-1224

このリリースは [Cloud Foundry community Node.js](https://github.com/cloudfoundry/nodejs-buildpack) ビルドパックと完全に同期しています。 コミュニティーの変更に加えて、特定のデフォルトに対する変更、ステージング時間を削減するための最適化、およびアプリケーション管理フィーチャーに対する更新が行われました。

* ビルドパック更新:

  * Node.js v4.2.4 (IBM SDK for Node.js バージョン 4) は現在 {{site.data.keyword.Bluemix_notm}} でのデフォルト・ランタイムであり、v0.12.9 を置き換えます。 この変更により、アプリケーションに対して特定のバージョンが指定されていない場合、アプリケーションが異なる動作をすることがあります。 {{site.data.keyword.Bluemix_notm}} アプリケーションに対して Node.js のバージョンを指定する方法については、[Node.js ランタイム](index.html)の資料を参照してください。

  * 現在、NODE_ENV はデフォルトで *production* に設定されています。 この変更により、一部のノード依存関係が異なる動作をするようになります。 例えば、Express フレームワークでは、障害のあるエンドポイントについて Web ブラウザーにスタック・トレースを返さなくなり、代わりに*内部サーバー・エラー*を表示します。 NPM_CONFIG_PRODUCTION が *true* に設定されている場合、NPM は、npm インストール・フェーズでのみ、サブシェル・スクリプトに対して NODE_ENV を *production* に設定します。 この機能により、ユーザーは、アプリケーション・ランタイムに対して NODE_ENV を *development* などの別の値に設定できるようになります。 明確にするために、npm スクリプトはメッセージ **NODE_ENV=production** を確認します。

  * Monitoring and Analytics サービスに対するバグ修正が組み込まれています。

* キャッシング更新:

  * キャッシュが無効になっている (NODE_MODULES_CACHE=false) 場合、ビルドパックはどのモジュールまたはコンポーネントのキャッシュも試行しません。 以前、この設定では、キャッシュはポップされませんでしたが、今後のデプロイに備えてインストール済みモジュールはキャッシュされていました。 現在は、キャッシュはポップされず、どのキャッシュの保管も試行されません。

  * デフォルトでは、node_modules に加えて Bower_components がキャッシュされます。

* その他の更新:

  * gulp、bower、および angular などの依存関係の欠落に対して、便利な警告が追加されました。

  * 検出スクリプトが、ビルドパック・バージョン情報によって更新されました。

  * コミュニティーによって当初紹介されていたクラスター化の推奨事項 (WEB_CONCURRENCY) は、メモリー決定が {{site.data.keyword.Bluemix_notm}} で不正確だったため削除されました。


## 2015 年 12 月 16 日: 更新された Node.js ビルドパック v2.8-20151209-1403 および v3.0beta-20151211-2041

このリリースの Node.js ビルドパックは、v2.8 および v3.0beta の 2 つのバージョンに付属しています。 これらのバージョンにはいずれも、以下の変更が含まれます。

Monitoring and Analytics サービスに対するバグ修正。
IBM SDK for Node.js v4.2.3.0、v4.2.2.0、v1.2.0.8、および v1.2.0.7 のキャッシュ付きランタイムの組み込み。これらは、コミュニティー・バージョンの Node.js v4.2.3、v4.2.2、v0.12.9、および v0.12.8 に基づいています。
さらに、v3.0beta で、デフォルトの Node.js ランタイムが v4.2.3 に変更されました。

IBM Node.js ビルドパック v3.0beta が、{{site.data.keyword.Bluemix_notm}} の非デフォルト・ビルドパックとしてリリースされました。このビルドパックでは、Node.js v4.2.3 をデフォルト・ランタイムとしています。 アプリケーションおよびサービスが引き続き {{site.data.keyword.Bluemix_notm}} 上で確実に機能するように、ベータ版のビルドパックを使用してアプリケーションをプッシュしてください。 30 日以上が経過すると、v3 がデフォルト・ビルドパックになります。

v3.0beta でアプリケーションをプッシュするには、以下を行います。
* `ibmcloud cf push` コマンドで「-b」オプションを使用します。

```
        ibmcloud cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}

* あるいは、manifest.yml ファイルで「buildpack」オプションを使用します。

```
        buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

アプリケーションの package.json で特定バージョンの Node.js を構成した場合、デフォルト・ランタイムに対するこの変更はアプリケーションには影響しません。

**注:** [『使用可能なバージョン』](index.html#available_versions)で説明されているように、package.json の engines.node 項目を使用して、アプリケーションを実行する Node.js のバージョンをいつでも指定できます。

## 2015 年 11 月 23 日: 更新された Node.js ビルドパック v2.7-20151118-1003

2.7 では、IBM SDK for Node.js のバージョン 4.2.1.0 が (Node v4.2.1 LTS に基づいて) 組み込まれています。 これはまだデフォルトではありませんが、使用対象として指定できます。 **注:** このバージョンは、以前に使用可能であったオープン・ソース・ビルドに取って代わります。 また、サービス拡張フレームワークに対していくつかの小さなバグ修正も行われています。

## 2015 年 10 月 19 日: 更新された Node.js ビルドパック v2.6.1-20151015-1326

Node.js v2.6.1 では、[StrongPM アプリケーション管理ハンドラー](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)に対するバグ修正と、より一貫性のある NPM バージョンが導入されています。

## 2015 年 10 月 15 日: 更新された Node.js ビルドパック v2.6-20151006-1309

このリリースの Node.js ビルドパックの特徴は、アプリケーション管理フィーチャーへの [StrongLoop Process Manager ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://strong-pm.io) の統合です。 詳しくは、ブログ投稿[『StrongLoop DevOps for Node.js Applications on {{site.data.keyword.Bluemix_notm}}』](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)を参照してください。

## 2015 年 6 月 15 日: 更新された Node.js ビルドパック v2.0-20150608-1503

このリリースでは、Node.js ビルドパックが、コミュニティーからの数多くの新しいフィーチャーが付属する最新の [CF コミュニティー Node.js ビルドパック](https://github.com/cloudfoundry/nodejs-buildpack)と同期化されています。
さらに、Node.js ビルドパックでアプリケーション管理フィーチャーが改訂されました。これにより、shell、node-inspector、{{site.data.keyword.Bluemix_notm}} Live Sync などのユーティリティーが使用可能になります。 詳しくは、[『アプリケーション管理』](../common/app_mng.html)を参照してください。

## 2015 年 5 月 5 日: 更新された Node.js ビルドパック v1.17-20150429-1033

* この Node.js ビルドパックには [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/) が付属するようになりました。
* アプリケーションの package.json ファイルでランタイムを指定していない場合、アプリケーションは v0.10.x の代わりに v0.12.1 を使用して開始されるようになります。 前のバージョンを使用する必要がある場合は、以下に示すように package.json で v0.10.x を指定してください。

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* v0.12.1 での既知の問題:
   * {{site.data.keyword.Bluemix_notm}} Live Sync で提供されるデバッグ・ツール・フィーチャーを使用すると、「中断」フィーチャーが失敗します。
   * MQ Light サービスで使用される mqlight モジュールは、v0.12.x ではサポートされません。

* 以下のような、さまざまなセキュリティー脆弱性が解決されました。
  * IBM SDK for Node.js に影響する OpenSSL での脆弱性が修正されました。 [『Security Bulletin』](http://www-01.ibm.com/support/docview.wss?uid=swg21701494)に詳細が記載されています。
  * IBM SDK for Node.js に影響する  RC4 ストリーム暗号での脆弱性が修正されました。 [『Security Bulletin』](http://www-01.ibm.com/support/docview.wss?uid=swg21882778)に詳細が記載されています。

##  2015 年 4 月 2 日: 更新された Node.js ビルドパック v1.15-20150331-2231

* Node.js ビルドパックには、再デプロイせずに、デスクトップで開発する場合と同様に {{site.data.keyword.Bluemix_notm}} で迅速に開発できるようにする、3 つの新しいフィーチャーが含まれるようになりました。
  * デスクトップ同期: 任意の (Windows) デスクトップ・ツリーをクラウド・ベースのプロジェクト・ワークスペースと同期化します。
  * ライブ編集: ご使用のブラウザーで、{{site.data.keyword.Bluemix_notm}} で実行される Node.js アプリケーションを変更して、直ちにテストできます。
  * デバッグ: 環境を準備してデバッグを行います。 Node Inspector デバッガーを使用して、コードの動的編集、ブレークポイントの挿入、コードのステップスルー、ランタイムの再始動などを行うことができます。
  * 詳しくは、[『アプリケーション管理』](../common/app_mng.html#Utilities)を参照してください。
* 最新の変更が [Cloud Foundry の Node.js ビルドパック](https://github.com/cloudfoundry/nodejs-buildpack)から導入されました。 この変更には、コミュニティーによって行われたいくつかのバグ修正および改善が付随しています。
* この Node.js ビルドパックには [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/) が付属するようになりました。

## 2015 年 1 月 5 日: 更新された Node.js ビルドパック v1.9.1-20141208-1221

* Node.js ビルドパックに動的ログ設定サポートが組み込まれました。 このサポートにより、アプリケーションがロギングに log4js、bunyan、または ibm{{site.data.keyword.Bluemix_notm}} の各モジュールを使用している場合、開発者はアプリケーションのログ・レベルを動的に変更することができます。
* この Node.js ビルドパックには [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/) が付属するようになりました。 この更新には、POODLE 問題の修正が含まれています。

## 2014 年 10 月 23 日: 更新された Node.js ビルドパック v1.6-20141013-1736

* この Node.js ビルドパックには [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/) が付属するようになりました。 この更新により、アプリケーション v0.10.32 に最新の安定した Node.js ランタイムを指定すると、完全にサポートされる IBM Node.js ランタイムが提供されるようになります。 この最新の SDK には、サービス妨害を起こす組み込み qs モジュールの問題
の修正が付属しています。 また、npm モジュールの更新版や、http および url モジュールの他の改善
も含まれています。 詳しくは、[v0.10.32 変更ログ](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog)を参照してください。
* このビルドパックには、デプロイメント中お客様のアプリケーションに間違
った index.html ファイルを追加するバグの修正も含まれています。

## 2014 年 9 月 30 日: 更新された Node.js ビルドパック v1.4-20140908-1746

* この Node.js ビルドパックには [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/) が付属するようになりました。 この更新により、アプリケーション v0.10.31 に最新の安定した Node.js ランタイムを指定すると、完全にサポートされる IBM Node.js ランタイムが提供されるようになります。 完全にサポートされる Node.js ランタイムを使用すると、お客様は一貫性のあるサポートを受けることができます。
* このビルドパックには、改善されたサービス・フレームワークが含まれています。 特に、Monitoring and Analytics サービスのバインド時の機能が向上しており、サーバーが失敗した場合に追加の診断情報が提供されます。

## 2014 年 8 月 28 日: 更新された Node.js ビルドパック v1.3-20140821-1143

* この最新の Node.js ビルドパックには IBM SDK for Node.js v1.1.0.6 が付属するようになりました。 この更新により、アプリケーション v0.10.30 に最新の安定した Node.js ランタイムを指定すると、完全にサポートされる IBM Node.js ランタイムが提供されるようになります。 このランタイムは、[V8 メモリー破壊脆弱性 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow) を修正します。
* また、このビルドパックには Monitoring and Analytics サービス拡張機能に対する改善およびバグ修正が含まれ、これによりサービス全体を通してパフォーマンスおよびエラー状態を診断することができます。

## 2014 年 7 月 29 日: 更新された Node.js ビルドパック v1.1-20140717-1447

この Node.js ビルドパックには IBM SDK for Node.js v1.1.0.5 が付属するようになりました。 この更新により、アプリケーション v0.10.29 に最新の安定した Node.js ランタイムを指定すると、完全にサポートされる IBM Node.js ランタイムが提供されるようになります。 詳細については [IBM Node.js SDK](https://developer.ibm.com/node/sdk/) を参照してください。
