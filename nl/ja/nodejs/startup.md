---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 開始コマンドの使用
{: #startup_commmand}

{{site.data.keyword.Bluemix}} Node.js アプリケーションの開始コマンドを指定する方法として推奨されるのは、**Procfile** ファイルまたは **package.json** ファイルのいずれかを使用することです。
{: shortdesc}

1. 下記の形式で、**Procfile** に開始コマンドを指定します。 ここで、_app.js_ は、アプリケーションの開始 js スクリプトです。
```
web: node app.js
```
{: codeblock}

1. **Procfile** をアプリケーションのルート・ディレクトリーに保存します。

**Procfile** が存在しない場合、{{site.data.keyword.Bluemix_notm}} Node.js ビルドパックによって、**package.json** ファイルに scripts.start エントリーがあるかどうかが検査されます。 下の例でも、app.js はアプリケーション用の開始 js スクリプトです。
```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

開始スクリプト項目が **package.json** にある場合は、**Procfile** が自動的に生成されます。 自動生成された **Procfile** の内容は次のようになります。
```
    web: npm start
```
{: codeblock}

**Procfile** および **package.json** ファイルについて詳しくは、[Tips for Node.js Applications ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html) を参照してください。
