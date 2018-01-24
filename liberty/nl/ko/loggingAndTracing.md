---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 로깅 및 추적 구성
{: #logging_tracing}

## 로그 파일
{: #log_files}

`messages.log` 또는 `ffdc` 디렉토리와 같은 표준 Liberty 로그는 각 애플리케이션 인스턴스의 `logs` 디렉토리에 있는 {{site.data.keyword.Bluemix}}에서 사용 가능합니다. 이러한 로그는 {{site.data.keyword.Bluemix_notm}} 콘솔 또는 Cloud Foundry CLI를 통해 액세스할 수 있습니다. 예:

* 앱의 최근 로그에 액세스하려면 다음 명령을 실행하십시오.

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* DEA 노드에서 실행 중인 앱의 `messages.log` 파일을 보려면 다음 명령을 실행하십시오.

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* Diego 노드에서 실행 중인 앱의 `messages.log` 파일을 보려면 다음 명령을 실행하십시오.

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

로그 레벨 및 다른 추적 옵션은 Liberty 구성 파일을 통해 설정할 수 있습니다. 자세한 정보는 [Liberty 문제점 해결: 로깅 및 추적](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)을 참조하십시오. {{site.data.keyword.Bluemix_notm}}
콘솔을 사용하여 실행 중인 애플리케이션 인스턴스에서 추적을 조정할 수도 있습니다.

## 추적 및 덤프 기능 사용
{: #using_trace_and_dump}

Liberty 추적 구성은 {{site.data.keyword.Bluemix_notm}} 콘솔에서 직접 실행 중인 애플리케이션에 맞게 조정 가능합니다. 또한 콘솔은 스레드 및 힙 덤프를 요청하고 다운로드하는 기능을 제공합니다. 추적 구성을 조정하거나 덤프를 요청하려면 {{site.data.keyword.Bluemix_notm}} 콘솔에서 Liberty 애플리케이션을 선택하고 탐색에서 `Runtime` 메뉴를 선택하십시오. `Runtime` 보기에서 인스턴스를 선택하고 *추적* 또는 *덤프* 단추를 누르십시오. 추적 레벨을 조정하는 경우 추적 스펙의 구문에 대한 세부사항은 [Liberty 문제점 해결: 로깅 및 추적](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)을 참조하십시오.

### Diego에서 SSH를 통해 추적 구성 변경

Diego 셀에서 실행 중인 Liberty 애플리케이션의 경우 SSH 기능을 사용하여 Cloud Foundy를 통해 추적 구성을 변경할 수 있습니다.

푸시된 애플리케이션은 **폴링** 값을 사용하여 **updateTrigger**가 포함된 server.xml을 포함시켜야 합니다. 그런 다음 런타임 환경에서 server.xml의 추적 스펙에 대한 변경사항이 발견되고 적용됩니다.

사용자 정의된 sever.xml을 사용하여 Liberty 앱을 푸시하는 옵션은 [server.xml을 사용하여 Liberty 앱 푸시](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing)를 참조하십시오. 

server.xml에서 동적 업데이트를 설정하는 방법은 [동적 업데이트 제어](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window}를 참조하십시오.

추적 구성을 변경하려면 다음 단계를 완료하십시오.

1. 앱에 SSH 실행

  ```
$ cf ssh <appname> [-i instance_index]
  ```
  {: pre}

2. server.xml에서 ```<logging traceSpecification="xxxx"/>```를 편집하여 원하는 추적 스펙을 설정하십시오. 예를 들어, *vi*를 사용합니다.

  ```
$ vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: pre}

참고: server.xml 변경사항은 다시 스테이징 및 다시 시작 시 유실되며 SSH를 실행하는 인스턴스에만 유효합니다.

추적 스펙의 구문에 대한 세부사항은 [Liberty 문제점 해결: 로깅 및 추적](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window}을 참조하십시오.

### Diego에서 SSH를 통해 덤프 트리거

Diego 셀에서 실행 중인 애플리케이션의 경우 SSH 기능을 사용하여 CF CLI를 통해 스레드 및 힙 덤프를 트리거할 수 있습니다. 예:

  ```
$ cf ssh <appname> -c "pkill -3 java"
  ```
  {: pre}

생성된 덤프 파일 다운로드에 대한 세부사항은 다음 문서를 참조하십시오.

## 덤프 파일 다운로드
{: #download_dumps}

기본적으로 다양한 덤프 파일이 애플리케이션 컨테이너의 `dumps` 디렉토리에 위치합니다.

### DEA 애플리케이션

DEA 노드에서 실행 중인 애플리케이션의 경우, "cf files" 기능을 사용하여 덤프 파일을 보고 다운로드하십시오.

* 생성된 덤프를 보려면 다음 명령을 실행하십시오.

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* 덤프 파일을 다운로드하려면 다음 명령을 실행하십시오.

    1. 애플리케이션 GUID 가져오기

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. 덤프 파일 다운로드

      ```
      $ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
      ```
      {: codeblock}

### Diego 애플리케이션

Diego 셀에서 실행 중인 애플리케이션의 경우, "cf ssh" 기능을 사용하여 덤프 파일을 보고 다운로드하십시오.

* 생성된 덤프를 보려면 다음 명령을 실행하십시오.

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* 덤프 파일을 다운로드하려면 다음 명령을 실행하십시오.

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

`scp` 및 기타 유사한 도구를 사용하여 덤프 파일을 보고 다운로드할 수 있습니다. 자세한 정보는 [Accessing Apps with SSH ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html)를 참조하십시오.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Liberty 런타임](index.html)
* [Liberty 개요](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
