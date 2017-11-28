---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# トラブルシューティングに関するよくある質問
{: #troubleshooting_faq}

**Q**: アプリケーションがデプロイに失敗し、メッセージ `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}` が出されます。これは何を意味するのでしょうか。

**A**: アプリケーションのプッシュ時にも同様のメッセージを受け取っている場合、最も考えられる原因は、ご使用のアプリケーションがメモリーまたはディスクの割り当て量制限を超えていることです。これは、アプリケーションに対する割り当て量を増やすことで解決できます。

**Q**: アプリケーションがデプロイに失敗し、「`Failed to compress droplet: signal: broken pipe`」または「`No space left on device`」というメッセージが出されます。これを修正する方法を教えてください。

**A**: 多数の NuGet パッケージ依存関係が含まれているソース・コードからプッシュされるプロジェクトでは、NuGet パッケージのキャッシュが有効になっている場合に、このエラーが発生することがあります。`CACHE_NUGET_PACKAGES` 環境変数を `false` に設定して、キャッシュを無効にしてください。詳しくは、[NuGet パッケージの無効化](diablingNuGet.md)の方法についての説明を参照してください。

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core Overview](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
