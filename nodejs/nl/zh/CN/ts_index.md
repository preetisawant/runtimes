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

# SDK for Node.js 故障诊断
{: #ts}


以下是对在 {{site.data.keyword.Bluemix}} 上使用 SDK for Node.js 的常见故障诊断问题的回答。
{:shortdesc}

要了解有关日志记录和跟踪的更多信息，请参阅[管理 Liberty 和 Node.js 应用程序](../../manageapps/app_mng.html)中的[跟踪](../../manageapps/app_mng.html#trace)部分。

## 应用程序未能启动，错误为“No space left on device”
{: #no_space_left_on_device}


Node.js 应用程序未能启动，错误为“No space left on device”。例如，日志中的错误可能看起来如下所示：
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

Node.js 应用程序使用的 NPM 版本如果早于 V3，下载依赖关系所消耗的空间就会更多。
{: tsCauses}

修改应用程序的 package.json 文件，以使用 NPM V3 或更高版本。
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

## 应用程序因内存约束而重新启动
{: #oom}

Node.js 不知道有多少内存可用于应用程序，所以在内存耗尽前垃圾回收器可能不会运行。

```
2017-09-01T11:00:42.19-0400 [APP/PROC/WEB/0]OUT Exit status 137
2017-09-01T11:00:42.23-0400 [CELL/0]     OUT Exit status 0
2017-09-01T11:00:42.27-0400 [CELL/0]     OUT Destroying container
2017-09-01T11:00:42.34-0400 [API/0]      OUT Process has crashed with type: "web"
2017-09-01T11:00:42.36-0400 [API/0]      OUT App instance exited with guid eecfba3b-430c-4a6b-b71f-ac72816fe152 payload: {"instance"=>"77dbb981-16d0-3a05-3235-9a4b", "index"=>0, "reason"=>"CRASHED", "exit_description"=>"2 error(s) occurred:\n\n* 2 error(s) occurred:\n\n* Exited with status 137 (out of memory)\n* cancelled\n* cancelled", "crash_count"=>1, "crash_timestamp"=>1504278042244633291, "version"=>"6497b5b5-67d4-4c5a-b1af-362e522a029d"}
2017-09-01T11:00:43.35-0400 [CELL/0]     OUT Successfully destroyed container
```
{: codeblock}

可能的解决方案是在 package.json 文件中应用程序的开始命令上设置 `--max_old_space_size` 选项。此选项表示应用程序内存覆盖区的一部分，因此应该设置为小于应用程序可用内存总量的值。请阅读[大内存峰值和 Heroku](https://github.com/nodejs/node/issues/3370)以了解有关此主题更深入的讨论。
```
  "scripts": {
    "start": "node --max_old_space_size=800 server.js"
  }
```
{: codeblock}
