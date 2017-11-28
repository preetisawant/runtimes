---

copyright:
  years: 2017
lastupdated: "2017-09-18"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# SDK for Node.js のトラブルシューティング
{: #ts}


ここでは、{{site.data.keyword.Bluemix}} 上での SDK for Node.js の使用に関する一般的なトラブルシューティングの質問に対する回答を示します。
{:shortdesc}

## 「No space left on device」エラーでアプリケーションが開始に失敗する
{: #no_space_left_on_device}


「No space left on device」エラーで、Node.js アプリケーションが開始に失敗します。例えば、ログ内のエラーは、次のようになっています。
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

NPM バージョン 3 より前のバージョンを使用している Node.js アプリケーションでは、依存関係のダウンロード時により多くのスペースを使用します。
{: tsCauses}

NPM バージョン 3 以上を使用するように、アプリケーションの package.json ファイルを変更してください。
{: tsResolve}

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}

## メモリーの制約が原因でアプリケーションが再始動する
{: #oom}

Node.js は、アプリケーションが使用可能なメモリー量を認識しないため、メモリーが使い尽くされる前にガーベッジ・コレクターが稼働しない可能性があります。

```
2017-09-01T11:00:42.19-0400 [APP/PROC/WEB/0]OUT Exit status 137
2017-09-01T11:00:42.23-0400 [CELL/0]     OUT Exit status 0
2017-09-01T11:00:42.27-0400 [CELL/0]     OUT Destroying container
2017-09-01T11:00:42.34-0400 [API/0]      OUT Process has crashed with type: "web"
2017-09-01T11:00:42.36-0400 [API/0]      OUT App instance exited with guid eecfba3b-430c-4a6b-b71f-ac72816fe152 payload: {"instance"=>"77dbb981-16d0-3a05-3235-9a4b", "index"=>0, "reason"=>"CRASHED", "exit_description"=>"2 error(s) occurred:\n\n* 2 error(s) occurred:\n\n* Exited with status 137 (out of memory)\n* cancelled\n* cancelled", "crash_count"=>1, "crash_timestamp"=>1504278042244633291, "version"=>"6497b5b5-67d4-4c5a-b1af-362e522a029d"}
2017-09-01T11:00:43.35-0400 [CELL/0]     OUT Successfully destroyed container
```
{: codeblock}

考えられる解決策の 1 つは、package.json ファイルでアプリケーションの開始コマンドに `--max_old_space_size` オプションを設定することです。このオプションは、アプリケーションのメモリー占有スペースの一部を表し、アプリケーションが使用可能な合計メモリーより少ない値に設定する必要があります。このトピックについての詳しい説明は、[Large memory spikes and Heroku](https://github.com/nodejs/node/issues/3370) をご覧ください。
```
  "scripts": {
    "start": "node --max_old_space_size=800 server.js"
  }
```
{: codeblock}
