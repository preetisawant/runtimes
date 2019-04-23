---

copyright:
  years: 2017, 2018
lastupdated: "2018-11-20"
subcollection: "Go"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# 시작하기 튜토리얼
{: #getting-started}

* {: download}축하합니다. {{site.data.keyword.Bluemix}}에 Hello World 샘플 애플리케이션을 배치했습니다.  시작하려면 이 단계별 안내서를 따르십시오. 또는 <a class="xref" href="http://bluemix.net" target="_blank" title="(샘플 코드 다운로드)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="애플리케이션 코드 다운로드" />샘플 코드를 다운로드</a>하고 직접 탐색하십시오.

이 시작하기 튜토리얼에 따라 개발 환경을 설정하고, 앱을 로컬 및 {{site.data.keyword.Bluemix}}에 배치하고, 앱에 {{site.data.keyword.Bluemix_notm}} 데이터베이스 서비스를 통합합니다.

이러한 문서에서 Cloud Foundry CLI에 대한 참조가 {{site.data.keyword.Bluemix_notm}} CLI로 업데이트되었습니다! {{site.data.keyword.Bluemix_notm}} CLI는 익숙한 Cloud Foundry 명령을 포함하고 있지만 {{site.data.keyword.Bluemix_notm}} 계정 및 기타 서비스와의 통합성 면에서는 더 낫습니다. 이 튜토리얼에서 {{site.data.keyword.Bluemix_notm}} CLI를 시작하는 방법에 대해 자세히 알아보십시오.
{: tip}

## 시작하기 전에
{: #prereqs}

다음이 필요합니다.
* [{{site.data.keyword.Bluemix_notm}} 계정](https://cloud.ibm.com/registration)
* [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/ibmcloud/download_cli.html)
* [Git ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://git-scm.com/downloads){: new_window}
* [Go ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://golang.org/dl/){: new_window}

## 1단계: 샘플 앱 복제
{: #clone}

1. 먼저 모든 GO 환경 변수가 올바르게 설정되어 있는지 확인하여 로컬 환경을 설정합니다. 예를 들어, 다음과 같습니다.

  ```
mkdir $HOME/work
export GOPATH=$HOME/work
export PATH=$PATH:$GOPATH/bin
  ```
  {: codeblock}

1. $GOPATH/src로 경로 변경

  ```
mkdir $GOPATH/src
cd $GOPATH/src
  ```
  {: codeblock}

  이제 단순 Go *hello world* 앱에 대한 작업을 시작할 준비가 되었습니다.
1. 저장소를 복제하고 샘플 앱이 있는 디렉토리로 변경하십시오.

  ```
go get github.com/IBM-Cloud/get-started-go
  ```
  {: codeblock}

  ```
cd github.com/IBM-Cloud/get-started-go
  ```
  {: codeblock}

1. **`get-started-go`** 디렉토리에서 파일을 확인하여 컨텐츠를 익히십시오.

## 2단계: 로컬에서 앱 실행
{: #run_locally}

1. 다음 명령을 실행하여 앱을 로컬에서 빌드하고 실행하십시오.

  ```
make
  ```
  {: codeblock}

  ```
go run main.go
  ```
  {: pre}

1. 다음 URL에서 앱을 확인하십시오. http://localhost:8080

앱을 시작한 동일한 창에서 앱을 중지하려면 *Ctrl-C*를 누르십시오.
{: tip}

## 3단계: 배치를 위한 앱 준비
{: #prepare}

{{site.data.keyword.Bluemix_notm}}에 배치하는 경우 manifest.yml 파일을 설정하는 것이 도움이 될 수 있습니다. manifest.yml에는 앱에 대한 기본 정보(예: 이름, 각 인스턴스에 할당할 메모리 크기, 라우트)가 포함됩니다. `get-started-go` 디렉토리에 샘플 manifest.yml 파일을 제공했습니다.

manifest.yml 파일을 열고 `name`을 `GetStartedGo`에서 앱 이름 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>으로 변경하십시오.
{: download}

  ```
 applications:
 - name: GetStartedGo
   random-route: true
   memory: 128M
   buildpack: go_buildpack
  ```
  {: codeblock}

이 manifest.yml 파일에서 **`random-route: true`**는 사용자 라우트가 다른 라우트와 충돌하지 않도록 앱을 위한 임의 라우트를 생성합니다.  원하는 경우, **`random-route: true`**를 **`host: myChosenHostName`**으로 바꾸고 사용하려는 호스트 이름을 제공할 수 있습니다.
{: tip}

## 4단계: 앱 배치
{: #deploy}

{{site.data.keyword.Bluemix_notm}} CLI를 사용하여 앱을 배치할 수 있습니다.

1. {{site.data.keyword.Bluemix_notm}} 계정에 로그인한 후 API 엔드포인트를 선택하십시오.

  ```
ibmcloud login
  ```
  {: codeblock}

  연합 사용자 ID가 있는 경우 대신 다음 명령을 사용하여 싱글 사인온 ID로 로그인하십시오. 자세한 정보는 [연합 ID로 로그인](/docs/cli/login_federated_id.html)을 참조하십시오.

  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Cloud Foundry 조직 및 영역 대상 지정:

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  조직이나 영역이 설정되지 않은 경우 [조직 및 영역 추가](/docs/account/orgs_spaces.html)를 참조하십시오.
  {: tip}

1. **`get-started-go`** 디렉토리 내에서 앱을 {{site.data.keyword.Bluemix_notm}}에 푸시

  ```
ibmcloud cf push
  ```
  {: codeblock}

  이를 수행하는 데 시간이 좀 걸릴 수 있습니다. 배치 프로세스에 오류가 있는 경우 `ibmcloud cf logs <Your-App-Name> --recent` 명령을 사용하여 문제점을 해결할 수 있습니다.

배치가 완료되면 앱이 실행 중이라는 메시지가 표시됩니다.  push 명령의 출력에 나열된 URL에서 앱을 확인하십시오. 다음 명령을 실행하여 앱 상태를 보고 URL을 확인할 수도 있습니다.

  ```
ibmcloud cf apps
  ```
  {: codeblock}

{{site.data.keyword.Bluemix_notm}} [리소스 목록](https://cloud.ibm.com/resources)으로 이동하여 앱을 볼 수도 있습니다.

## 5단계: 데이터베이스 추가
{: #add_database}

다음으로, 이 애플리케이션에 {{site.data.keyword.cloudant_short_notm}} NoSQL 데이터베이스를 추가하고 애플리케이션을 설정하여 로컬 및 {{site.data.keyword.Bluemix_notm}}에서 이를 실행할 수 있도록 합니다.

1. 브라우저에서 {{site.data.keyword.Bluemix_notm}}에 로그인하고 대시보드로 이동하십시오. **리소스 작성**을 선택하십시오.
1. **{{site.data.keyword.cloudant_short_notm}}**를 검색한 후 서비스를 선택하십시오.
1. **사용 가능한 인증 방법**의 경우 **레거시 인증 정보 및 IAM 모두 사용**을 선택하십시오. 다른 필드에서는 기본 설정을 유지할 수 있습니다. **작성**을 클릭하여 서비스를 작성하십시오.
1. 탐색에서 **연결**로 이동한 후 **연결 작성**을 클릭하십시오. 애플리케이션을 선택한 후 **연결**을 클릭하십시오.
1. 기본값을 사용하고 **연결 & 앱 다시 스테이징**을 클릭하여 데이터베이스를 애플리케이션에 연결하십시오. 프롬프트가 표시되면 **다시 스테이징**을 클릭하십시오.

   {{site.data.keyword.Bluemix_notm}}가 애플리케이션을 다시 시작하고, `VCAP_SERVICES` 환경 변수를 사용하여 애플리케이션에 데이터베이스 인증 정보를 제공합니다. 이 환경 변수는 {{site.data.keyword.Bluemix_notm}}에서 실행 중인 경우에만 애플리케이션에서 사용 가능합니다.

환경 변수를 사용하면 배치 설정을 소스 코드와 구분할 수 있습니다. 예를 들어, 데이터베이스 비밀번호를 하드 코딩하는 대신 소스 코드에서 참조하는 환경 변수에 이를 저장할 수 있습니다.
{: tip}

## 6단계: 데이터베이스 사용
{: #use_database}
이제 이 데이터베이스를 가리키도록 로컬 코드를 업데이트합니다. 애플리케이션이 사용할 서비스의 인증 정보를 저장할 .env 파일을 작성합니다. 이 파일은 애플리케이션이 로컬에서 실행 중인 경우에만 사용됩니다. {{site.data.keyword.Bluemix_notm}}에서 실행 중인 경우 인증 정보는 VCAP_SERVICES 환경 변수에서 읽습니다.

1. 다음 컨텐츠를 포함한 `get-started-go` 디렉토리의 `.env` 파일을 작성하십시오.

  ```
  CLOUDANT_URL=
  ```
  {: codeblock}

2. {{site.data.keyword.Bluemix_notm}} [리소스 목록](https://cloud.ibm.com/resources)에서 앱을 찾으십시오. 앱의 서비스 세부사항 페이지에 있는 사이드바에서 **연결**을 클릭하십시오. {{site.data.keyword.cloudant_short_notm}} 메뉴 아이콘(**&hellip;**)을 클릭하고 **인증 정보**를 선택하십시오.

3. 인증 정보의 `url`을 복사하여 `.env` 파일의 `CLOUDANT_URL` 필드에 붙여넣고 변경사항을 저장하십시오.  결과는 다음과 비슷합니다.

  ```
  CLOUDANT_URL=https://123456789 ... bluemix.cloudant.com
  ```
  {: codeblock}

4. 애플리케이션을 로컬에서 실행하십시오.

  ```
go run main.go
  ```
  {: codeblock}

  다음에서 앱을 확인하십시오. http://localhost:8080 이제 앱에 입력한 이름이 데이터베이스에 추가됩니다.

로컬 앱과 {{site.data.keyword.Bluemix_notm}} 앱은 데이터베이스를 공유합니다.  위에서 push 명령의 출력에 나열된 URL을 통해 {{site.data.keyword.Bluemix_notm}} 앱을 확인하십시오.  이 중 하나의 앱에서 추가하는 이름은 브라우저를 새로 고치면 두 앱에 모두 표시됩니다.


앱을 지속할 필요가 없는 경우 예상치 않은 비용이 발생하지 않도록 앱을 중지하십시오.
{: tip}

## 다음 단계

* [튜토리얼](/docs/tutorials/index.html)
* [샘플 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://ibm-cloud.github.io){: new_window}
* [아키텍처 센터 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
