---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-19"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core
{: #dotnet_core}

{{site.data.keyword.Bluemix}} の ASP.NET Core ランタイムには ASP.NET Core ビルドパックが採用されています。ASP.NET Core は、.NET Web アプリケーションをビルドするためのオープン・ソースのモジュラー・フレームワークです。
.Net Core は、ASP.NET Core アプリケーションのターゲットにできる小規模なクロスプラットフォーム・ランタイムです。
この組み合わせによって、最新のクラウド・ベース Web アプリケーションが使用可能になります。
{: shortdesc}

## 検出
{: #detection}
アプリケーションのどこかに project.json ファイルと少なくとも 1 つの .cs ファイルの両方を含むフォルダーが 1 つ以上存在する場合、あるいはアプリケーションが *dotnet publish* コマンドの出力ディレクトリーからプッシュされた場合、Bluemix ASP.NET Core ビルドパックが使用されます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、ASP.NET Core スターター・アプリケーションが用意されています。ASP.NET Core スターター・アプリケーションは、使用可能なテンプレートを提供する、シンプルなアプリケーションです。スターター・アプリケーションを試し、Bluemix 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](/docs/cfapps/starter_app_usage.html)を参照してください。

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core Overview](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
