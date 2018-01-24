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

# SDK for Node.js 문제점 해결
{: #ts}


다음은 {{site.data.keyword.Bluemix}}의 SDK for Node.js 사용과 관련된 일반적인 문제점 해결 질문에 대한 답입니다.
{:shortdesc}

로깅과 추적에 대해 자세히 보려면 [Liberty 및 Node.js 애플리케이션 관리](../../manageapps/app_mng.html)의 [추적](../../manageapps/app_mng.html#trace) 섹션을 참조하십시오.

## 애플리케이션이 시작에 실패하며 “No space left on device” 오류 발생
{: #no_space_left_on_device}


Node.js 애플리케이션이 시작에 실패하며 “No space left on device” 오류가 나타납니다. 예를 들면, 로그에 다음과 같은 오류가 표시됩니다.
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

버전 3 이전의 NPM 버전을 사용하는 Node.js 애플리케이션은 종속 항목 다운로드에 추가 공간을 사용합니다.
{: tsCauses}

애플리케이션의 package.json 파일을 수정하여 NPM 버전 3 이상을 사용하십시오.
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

## 메모리 제한조건으로 인해 애플리케이션 다시 시작
{: #oom}

Node.js에서는 애플리케이션에 사용 가능한 메모리의 양을 알 수 없기 때문에 메모리가 모두 사용되기 전에 가비지 콜렉터가 실행되지 않을 수 있습니다.

```
2017-09-01T11:00:42.19-0400 [APP/PROC/WEB/0]OUT Exit status 137
2017-09-01T11:00:42.23-0400 [CELL/0]     OUT Exit status 0
2017-09-01T11:00:42.27-0400 [CELL/0]     OUT Destroying container
2017-09-01T11:00:42.34-0400 [API/0]      OUT Process has crashed with type: "web"
2017-09-01T11:00:42.36-0400 [API/0]      OUT App instance exited with guid eecfba3b-430c-4a6b-b71f-ac72816fe152 payload: {"instance"=>"77dbb981-16d0-3a05-3235-9a4b", "index"=>0, "reason"=>"CRASHED", "exit_description"=>"2 error(s) occurred:\n\n* 2 error(s) occurred:\n\n* Exited with status 137 (out of memory)\n* cancelled\n* cancelled", "crash_count"=>1, "crash_timestamp"=>1504278042244633291, "version"=>"6497b5b5-67d4-4c5a-b1af-362e522a029d"}
2017-09-01T11:00:43.35-0400 [CELL/0]     OUT Successfully destroyed container
```
{: codeblock}

가능한 솔루션은 package.json 파일의 애플리케이션의 시작 솔루션에 `--max_old_space_size` 옵션을 설정하는 것입니다. 이 옵션은 애플리케이션 메모리 공간의 부분을 표시하고 애플리케이션에 사용 가능한 전체 메모리 미만으로 값을 설정해야 합니다. 이 주제에 대한 심도 깊은 토론을 보려면 [Large memory spikes and Heroku](https://github.com/nodejs/node/issues/3370)를 읽어 보십시오.
```
  "scripts": {
    "start": "node --max_old_space_size=800 server.js"
  }
```
{: codeblock}
