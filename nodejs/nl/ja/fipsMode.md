---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# FIPS モード
{: #fips_mode}

Node.js ビルドパックのバージョン v3.2-20160315-1257 から v3.20.2-20180523-1639 では、[FIPS ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards) がサポートされます。  
{: shortdesc}

**OpenSSL FIPS モジュールは非推奨です。** Node.js ビルドパック v3.22 以降、OpenSSL FIPS モジュールは、ランタイムのバージョン 6.x および 8.x で使用できなくなりました。バージョン4.x にのみ、引き続き OpenSSL FIPS モジュールが含まれます。詳しくは、[Node.js ビルドパックに対する最新の更新](updates.html#fips-deprecation)を参照してください。

FIPS 対応ノード・エンジンを使用するには、環境変数 FIPS_MODE を true に設定します。
例えば、次のとおりです。

```
    ibmcloud cf set-env myapp FIPS_MODE true
```
{: codeblock}

FIPS_MODE が true の場合、一部のノード・モジュールが機能しない可能性があることを認識しておくことが重要です。  例えば、[Express ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://expressjs.com/)のように、**[MD5 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://en.wikipedia.org/wiki/MD5)を使用するノード・モジュールは失敗します**。  Express の場合、Express アプリケーションで [etag ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://expressjs.com/en/api.html) を false に設定すると、こうした失敗を回避するのに役立つことがあります。 例えば、コードで以下のようにすることができます。
```
    app.set('etag', false);
```
{: codeblock}
詳しくは、[スタック・オーバーフローの投稿 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js) を参照してください。

**注:** [アプリケーション管理](../common/app_mng.html)と FIPS_MODE は、同時にはサポートされ*ません*。  BLUEMIX_APP_MGMT_ENABLE 環境変数が設定され、かつ FIPS_MODE 環境変数が true に設定されると、アプリケーションはステージングに失敗します。

FIPS_MODE の状態を確認するには、以下のようにさまざまな方法があります。
<ul>
<li> アプリケーションのログで、以下に似たメッセージがないかチェックします。    

  <pre>
  Installing FIPS-enabled IBM SDK for Node.js (4.4.3) from cache
  </pre>
  {: codeblock}

このメッセージは、FIPS 対応の node.js エンジンが実行中であるが、必ずしもその FIPS が実行されているとは限らないことを示します。
</li>

<li> **process.versions.openssl** の値を確認できます。 例えば、次のとおりです。

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

SSL バージョンに「fips」が含まれている場合、使用されているバージョンの SSL は FIPS をサポートしています。  
</li>

<li> node.js バージョン 6 以降の場合、以下のようなコードで crypto.fips によって返された値を確認できます。

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

戻り値が 1 の場合は、FIPS が使用されています。 なお、node.js バージョン 6 より前では、crypto.fips は *undefined* を返します。
</li>
</ul>

## Nodejs v4
{: #nodejs_v4_fips}

次の表は、FIPS を使用する node.js v4 の動作を説明しています。

|                 | 結果        |
| :-------------- | :------------ |
|FIPS_MODE=true   |成功 (1)    |
|FIPS_MODE !=true |成功 (2)    |

* 成功 (1)
  * FIPS は使用中です。
  * ログにメッセージ *Installing FIPS-enabled IBM SDK for Node.js* が含まれます。
  * process.versions.openssl によって返される値に「fips」が含まれます。
* 成功 (2)
  * FIPS は使用されて*いません*。
  * ログに、メッセージ *Installing FIPS-enabled IBM SDK for Node.js* は含まれ*ません*。
  * process.versions.openssl によって返される値に「fips」は含まれ*ません*。

## Node.js v6 以降
{: #nodejs_v6_fips}

Node.js バージョン 6 以降を使用して FIPS モードで実行するには、**FIPS_MODE=true** の設定に加えて、次の例のように、開始コマンドに **--enable-fips** を含める必要もあります。
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

次の表は、FIPS を使用する node.js v6 以降の動作を説明しています。

|                 |--enable-fips  |--enable-fips なし |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |成功 (1)    |成功 (2)      |
|FIPS_MODE !=true |失敗 (3)    |成功 (4)      |

* 成功 (1)
  * FIPS は使用中です。
  * ログにメッセージ *Installing FIPS-enabled IBM SDK for Node.js* が含まれます。
  * process.versions.openssl によって返される値に「fips」が含まれます。
  * crypto.fips は 1 を返し、FIPS が使用中であることを示します。
* 成功 (2)
  * FIPS は使用されて*いません*。
  * ログにメッセージ *Installing FIPS-enabled IBM SDK for Node.js* が含まれます。
  * process.versions.openssl によって返される値に「fips」が含まれます。
  * crypto.fips は 0 を返し、FIPS が使用されて*いない*ことを示します。
* 失敗 (3)
  * FIPS は使用されて*いません*。
  * ログに、メッセージ *Installing FIPS-enabled IBM SDK for Node.js* は含まれ*ません*。
  * ステージングは失敗し、メッセージ「ERR node: bad option: --enable-fips」が出されます。
* 成功 (4)
  * FIPS は使用されて*いません*。
  * ログに、メッセージ *Installing FIPS-enabled IBM SDK for Node.js* は含まれ*ません*。
  * process.versions.openssl によって返される値に「fips」は含まれ*ません*。
  * crypto.fips は 0 を返し、FIPS が使用されて*いない*ことを示します。
