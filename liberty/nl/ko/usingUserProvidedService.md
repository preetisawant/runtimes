---

copyright:
  years: 2017, 2018
lastupdated: "2018-6-26"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

#{{site.data.keyword.cloud_notm}}에서 Liberty와 함께 사용자 제공 서비스 사용
{: #using_user_provided}

Cloud Foundry는 {{site.data.keyword.Bluemix_notm}} 환경에 제공되지 않았거나
이 환경에서 사용 가능하지 않은 서비스에 연결하여 이를 사용하는 메커니즘을 제공합니다.
이 기능을 [사용자 제공 서비스](https://docs.cloudfoundry.org/devguide/services/user-provided.html)라고 합니다. 

이 문서에서는 다음 항목을 가정합니다. 
  * 사용자에게 몇 가지 사용 가능한 서비스가 있습니다. 
  * 사용자가 해당 서비스에 대한 인증 정보를 획득할 수 있으며,
Getting-Started-Liberty 샘플 애플리케이션을 사용해 해당 서비스에 연결하여
이를 사용하는 데 필요한 단계에 대한 설명이 제공됩니다. 

여기서는 이 토론을 위해 CloudantNoSQLDB 인스턴스를 서비스 예로 사용하고,
여기에 연결하기 위한 사용자 제공 서비스를 작성합니다. 

## 1단계: Getting-Started 애플리케이션 푸시
{: #follow_getting_started}

애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 푸시하는 부분까지
[시작하기 튜토리얼](/docs/runtimes/liberty/getting-started.html)의 단계를 따르십시오. 데이터베이스에 연결하는 부분 앞에서 단계를 중지하십시오. 

## 2단계: CloudantNoSQLDB 인스턴스 작성
{: #create_cloudantnosqldb}

[시작하기 튜토리얼](/docs/runtimes/liberty/getting-started.html)의 단계에 따라
CloudantNoSqLDB 인스턴스를 작성하십시오. 

인증 정보 보기 옵션을 사용하여 인증 정보를 CloudandNoSQLDB로 복사하십시오. 이러한 인증 정보를 cloudant-creds와 같은 로컬 파일에 저장하십시오. 

## 3단계: 사용자 제공 서비스 작성
Getting-Started 애플리케이션과 함께 작동하려면
사용자 제공 서비스의 이름이 "cloudantNoSQLDB"를
포함해야 합니다. Getting-Started 애플리케이션은
VCAP 서비스 변수를 구문 분석하며 "cloudantNoSQLDB"를
포함하는 이름을 가진 사용자 제공 서비스를 찾습니다. 

        ibmcloud cf cups my-cloudantNoSQLDB-ups -p cloudant-creds

## 4단계: 사용자 제공 서비스를 바인드하고 앱을 다시 스테이징
사용자 제공 서비스를 Getting-Started 애플리케이션에 바인드하십시오. 

        ibmcloud cf bs GettingStartedLiberty my-cloudantNoSQLDB-ups

        ibmcloud cf restage GettingStartedLiberty

## 5단계: 확인
애플리케이션을 탐색하여 '이름' 필드에
여러 이름을 추가할 수 있는지 확인하십시오. 
