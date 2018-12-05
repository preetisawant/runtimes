---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 로깅 및 추적 구성
{: #logging_tracing}

## 로그 파일
{: #log_files}

`messages.log` 또는 `ffdc` 디렉토리와 같은 표준 Liberty 로그는 각 애플리케이션 인스턴스의 `logs` 디렉토리에 있는 {{site.data.keyword.Bluemix}}에서 사용 가능합니다. 이러한 로그는 {{site.data.keyword.Bluemix_notm}} 콘솔 또는 {{site.data.keyword.Bluemix_notm}} CLI를 통해 액세스할 수 있습니다. 예를 들어, 다음과 같습니다.

* 앱의 최근 로그에 액세스하려면 다음 명령을 실행하십시오.

  ```
  ibmcloud cf logs --recent <appname>
  ```
  {: codeblock}


* 앱의 `messages.log` 파일을 보려면 다음 명령을 실행하십시오.

  ```
  ibmcloud cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

로그 레벨 및 다른 추적 옵션은 Liberty 구성 파일을 통해 설정할 수 있습니다. 자세한 정보는 [Liberty 문제점 해결: 로깅 및 추적](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)을 참조하십시오.

## 추적 및 덤프 기능 사용
{: #using_trace_and_dump}

### {{site.data.keyword.Bluemix_notm}} 콘솔에서 추적 및 덤프 사용(더 이상 사용되지 않음)

Liberty 추적 구성은 {{site.data.keyword.Bluemix_notm}} 콘솔에서 직접 실행 중인 애플리케이션에 맞게 조정 가능합니다. 또한 콘솔은 스레드 및 힙 덤프를 요청하고 다운로드하는 기능을 제공합니다. 추적 구성을 조정하거나 덤프를 요청하려면 {{site.data.keyword.Bluemix_notm}} 콘솔에서 Liberty 애플리케이션을 선택하고 탐색에서 `Runtime` 메뉴를 선택하십시오. `Runtime` 보기에서 인스턴스를 선택하고 *추적* 또는 *덤프* 단추를 누르십시오. 추적 레벨을 조정하는 경우 추적 스펙의 구문에 대한 세부사항은 [Liberty 문제점 해결: 로깅 및 추적](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)을 참조하십시오.

### SSH를 통한 추적 구성 변경

애플리케이션을 푸시하면 server.xml 파일에 **polled**로 설정된 기본 특성 **updateTrigger**와 1분으로 설정된 기본 설정 **monitorInterval**이 포함됩니다. Liberty 서버는 매분 server.xml 파일의 업데이트를 확인하도록 자동으로 구성됩니다.

사용자 정의된 `server.xml` 파일을 사용하여 Liberty 앱을 푸시하는 옵션은 [server.xml을 사용하여 Liberty 앱 푸시](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing)를 참조하십시오.

server.xml 파일에서 동적 업데이트를 설정하는 방법은 [동적 업데이트 제어](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window}를 참조하십시오.

추적 구성을 변경하려면 다음 단계를 따르십시오.

1. 앱에 SSH 실행

  ```
 ibmcloud cf ssh <appname> [-i instance_index]
  ```
  {: codeblock}

2. server.xml에서 `<logging traceSpecification="xxxx"/>`를 편집하여 원하는 추적 스펙을 설정하십시오. 예를 들어, *vi*를 사용합니다.

  ```
vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: codeblock}

참고: server.xml 변경사항은 다시 스테이징 및 다시 시작 시 유실되며 SSH를 실행하는 인스턴스에만 유효합니다.

추적 스펙의 구문에 대한 세부사항은 [Liberty 문제점 해결: 로깅 및 추적](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window}을 참조하십시오.

### SSH를 통한 덤프 트리거링

SSH 기능을 사용하여 {{site.data.keyword.Bluemix_notm}} CLI를 통해 스레드 및 힙 덤프를 트리거하려면 아래의 명령을 사용하십시오.

  ```
 ibmcloud cf ssh <appname> -c "pkill -3 java"
  ```
  {: codeblock}

생성된 덤프 파일 다운로드에 대한 세부사항은 다음 문서를 참조하십시오.

## 덤프 파일 다운로드
{: #download_dumps}

기본적으로 다양한 덤프 파일이 애플리케이션 컨테이너의 `dumps` 디렉토리에 위치합니다. {{site.data.keyword.Bluemix_notm}} CLI `ibmcloud cf ssh`를 사용하여 덤프 파일을 보고 다운로드하십시오.

* 생성된 덤프를 보려면 다음 명령을 실행하십시오.

  ```
  ibmcloud cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* 덤프 파일을 다운로드하려면 다음 명령을 실행하십시오.

  ```
  ibmcloud cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

`scp` 및 기타 유사한 도구를 사용하여 덤프 파일을 보고 다운로드할 수 있습니다. 자세한 정보는 [Accessing Apps with SSH ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html)를 참조하십시오.
