---

copyright:
  years: 2015, 2018
lastupdated: "2017-05-31"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# NuGet パッケージ・ソースのカスタマイズ
{: #customizing_nuget}

アプリケーションのルート・ディレクトリー内の `NuGet.Config` ファイルを使用して、アプリケーションが依存関係をダウンロードする場所を制御できます。 次の例では、`<packageSources>` プロパティーを構成することで、アプリケーションがパッケージを取り出すためのキーおよび API URL を定義しています。
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}
