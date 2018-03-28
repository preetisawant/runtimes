---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Node.js アプリケーションのローカルでの実行
{: #hints}

Node.js アプリケーションを {{site.data.keyword.Bluemix}} で実行する際に、競合を引き起こさずにこのアプリケーションをローカルで実行するようにポート番号を設定します。
{: shortdesc}

アプリケーションが {{site.data.keyword.Bluemix_notm}} で実行されている場合、PORT 環境変数は Cloud Foundry によって割り振られます。 ただし、アプリケーションがローカルで実行されている場合、PORT は定義されないため、ユーザーがアプリケーションのポートを定義できます。 競合を避けるには、アプリケーションがローカルで listen するポートを、{{site.data.keyword.Bluemix_notm}} によって使用されるポートとは異なるポートに定義します。

**js** ファイルの次の例では、**3000** がポート番号として使用されています。 **3000** を使用することで、変更を行わずに、アプリケーションをテストのためにローカルで実行したり {{site.data.keyword.Bluemix_notm}} で実行したりすることができます。

```
var port = (process.env.PORT || 3000);
```
{: codeblock}
