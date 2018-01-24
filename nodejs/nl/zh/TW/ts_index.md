---

copyright:
  years: 2017
lastupdated: "2017-12-15"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# SDK for Node.js 疑難排解
{: #ts}


以下是有關在 {{site.data.keyword.Bluemix}} 上使用 SDK for Node.js 的常見疑難排解問題的答案。
{:shortdesc}

若要進一步瞭解記載和追蹤，請參閱[管理 Liberty 及 Node.js 應用程式](../../manageapps/app_mng.html)中的[追蹤](../../manageapps/app_mng.html#trace)一節。

## 應用程式無法啟動，錯誤為「裝置上沒有可用的空間」
{: #no_space_left_on_device}


Node.js 應用程式無法啟動，錯誤為「裝置上沒有可用的空間」。例如，日誌中的錯誤可能類似下列內容：
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

下載相依關係時，使用第 3 版之前的 NPM 版本的 Node.js 應用程式會耗用更多空間。
{: tsCauses}

修改應用程式的 package.json 檔案，以使用 NPM 第 3 版或以上版本。
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

## 應用程式由於記憶體限制而重新啟動
{: #oom}

Node.js 不知道應用程式所能使用的記憶體數量，因此記憶體回收器可能不會在耗盡記憶體之前執行。

```
2017-09-01T11:00:42.19-0400 [APP/PROC/WEB/0]OUT Exit status 137
2017-09-01T11:00:42.23-0400 [CELL/0]     OUT Exit status 0
2017-09-01T11:00:42.27-0400 [CELL/0]     OUT Destroying container
2017-09-01T11:00:42.34-0400 [API/0]      OUT Process has crashed with type: "web"
2017-09-01T11:00:42.36-0400 [API/0]      OUT App instance exited with guid eecfba3b-430c-4a6b-b71f-ac72816fe152 payload: {"instance"=>"77dbb981-16d0-3a05-3235-9a4b", "index"=>0, "reason"=>"CRASHED", "exit_description"=>"2 error(s) occurred:\n\n* 2 error(s) occurred:\n\n* Exited with status 137 (out of memory)\n* cancelled\n* cancelled", "crash_count"=>1, "crash_timestamp"=>1504278042244633291, "version"=>"6497b5b5-67d4-4c5a-b1af-362e522a029d"}
2017-09-01T11:00:43.35-0400 [CELL/0]     OUT Successfully destroyed container
```
{: codeblock}

可行的解決方案是在 package.json 檔案的應用程式啟動指令上設定 `--max_old_space_size` 選項。此選項代表屬於應用程式一部分的記憶體覆蓋區，且應設為小於應用程式可用總記憶體的值。如需此主題的更深入討論，請閱讀 [Large memory spikes and Heroku](https://github.com/nodejs/node/issues/3370)。
```
  "scripts": {
    "start": "node --max_old_space_size=800 server.js"
  }
```
{: codeblock}
