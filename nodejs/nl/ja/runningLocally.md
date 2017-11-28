---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Node.js アプリケーションのローカルでの実行
{: #hints}

この情報を使用することで、Node.js アプリケーションのローカル側および {{site.data.keyword.Bluemix}} 上での実行が容易になります。
{: shortdesc}

次の例は、**js** ファイルのソースの一部を示しています。

```
var port = (process.env.PORT || 3000);
```
{: codeblock}

このコードでは、アプリケーションが Bluemix 上で実行されている場合、PORT 環境変数には、アプリケーションが着信接続を listen する Bluemix 内部のポート値が入ります。アプリケーションがローカルに実行される場合、PORT は定義されないため、ポート番号として **3000** が使用されます。このような方法でコードを書くと、アプリケーションをテスト目的でローカルに実行でき、またさらに変更を行うことなく Bluemix 上で実行できます。
