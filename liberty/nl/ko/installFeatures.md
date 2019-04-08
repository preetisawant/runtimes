---

copyright:
  years: 2018
lastupdated: "2018-12-14"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# Liberty 기능 설치
{: #install-features}

Liberty for Java 런타임에는 Liberty 기능에 사용 가능한 [기능의 서브세트](libertyFeatures.html#liberty_features)가 포함되어 있습니다. 애플리케이션이 {{site.data.keyword.cloud_notm}}에 푸시될 때 Cloud Foundry 사전 런타임 후크로 Liberty `installUtility` 명령을 실행하여 런타임에 포함되지 않는 기능을 설치할 수 있습니다.

사용 가능한 기능의 전체 목록은 [Liberty 기능 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)을 참조하십시오.

사전 런타임 후크 사용에 대한 정보는 Cloud Foundry 문서의 [사전 런타임 후크 구성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.cloudfoundry.org/devguide/deploy-apps/deploy-app.html#profile)을 참조하십시오.

1. {{site.data.keyword.cloud_notm}}에 푸시할 애플리케이션의 루트 디렉토리에서 `.profile.d` 디렉토리를 작성하십시오.

1. `.profile.d` 디렉토리에서 다음 예제와 같이 `installUtility` 명령을 실행하는 스크립트 파일을 작성하십시오.

   이 예는 `audit-1.0` 기능을 설치합니다.

   ```
   #!/bin/sh
   echo "Installing audit-1.0"
   export PATH=$PATH:$HOME/.java/jre/bin

   $HOME/.liberty/bin/installUtility install audit-1.0 --acceptLicense
   ```
   {: codeblock}

   공백으로 구분된 추가 기능 이름을 지정하여 다중 기능을 설치할 수 있습니다.
   {: tip}

1. 애플리케이션의 루트 디렉토리를 지정하려면 `-p` 매개변수를 사용하여 {{site.data.keyword.cloud_notm}}에 앱을 푸시하십시오.

   예를 들어, 앱을 푸시하려면 다음 명령을 실행하십시오.
   ```
   ibmcloud cf push myApp -p /<path-to-application>
   ```
   {: codeblock}

1. 애플리케이션의 최신 로그를 보고 기능이 설치되었는지 확인하십시오.

   예를 들어, 로그를 표시하려면 다음 명령을 실행하십시오.
   ```
   ibmcloud cf logs myApp --recent
   ```
   {: codeblock}

    기능이 설치된 경우 출력에는 다음 메시지가 표시됩니다.

    ```
    2018-09-18T13:01:17.61-0400 [APP/PROC/WEB/0] OUT audit-1.0 설치 중
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT 구성된 저장소에 대한 연결 설정 중...
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT 이 프로세스를 완료하는 데 몇 분이 걸릴 수 있습니다.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT 구성된 모든 저장소에 연결되었습니다.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT 설치를 위해 자산을 준비 중입니다. 이 프로세스를 완료하는 데 몇 분이 걸릴 수 있습니다.
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT --acceptLicense 인수가 발견되었습니다. 이는 라이센스 계약의
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT 조항에 동의했음을 나타냅니다.
    ```
