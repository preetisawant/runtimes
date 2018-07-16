---

copyright:
  years: 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dynatrace를 사용하여 {{site.data.keyword.cloud_notm}}의 Node.js 모니터링
{: #using_dynatrace}

Dynatrace는 앱에 대한 모니터링을 제공하는 써드파티 서비스입니다. Dynatrace를 Node.js 애플리케이션과 통합할 수 있지만 IBM에서는 써드파티 서비스에 대한 지원을 제공하지 않습니다. 자세한 정보는 [써드파티 서비스](../common/buildpackSupport.html#third-party)를 참조하십시오.

Dynatrace 및 해당 라이센싱에 대한 정보는 [Dynatrace 애플리케이션 모니터링 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.dynatrace.com/en/products/application-monitoring.html)을 참조하십시오.

Dynatrace를 사용하도록 Node.js 애플리케이션을 구성하는 경우 Node.js 런타임은 Dynatrace 사이트에서 Dynatrace PaaS(platform as a service) 설치 스크립트를 가져와서 해당 Dynatrace 에이전트를 사용자 앱에서 실행합니다. Dynatrace를 앱과 통합하려면 사용자 제공 서비스를 작성한 다음 서비스를 사용자 앱에 바인드해야 합니다.

## Dynatrace를 사용자 애플리케이션과 통합

1. Dynatrace 계정에 로그인하여 PaaS 토큰을 생성하십시오. 세부사항은 Dynatrace Cloud Foundry 앱 모니터링 문서에서 [PaaS 토큰 생성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/how-do-i-monitor-cloud-foundry-applications/) 절을 참조하십시오.

  환경 ID 및 토큰을 적어 두십시오.
1. 다음 명령을 실행하여 Dynatrace 신임 정보를 가리키는 사용자 제공 서비스를 작성하십시오. 서비스 이름에는 `dynatrace` 문자열이 포함되어야 합니다(예: `dynatrace-service`).

    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken"
    ```
    {: codeblock}
    
    **참고:** `environmentid` 또는 `apitoken`을 신임 정보와 바꾸지 마십시오. 명령을 실행하면 해당 값을 입력하라는 프롬프트가 표시됩니다.

    Dynatrace Managed를 사용하는 경우 `apiurl` 필드도 추가하십시오. 이 필드는 관리 서버의 API 엔드포인트를 지정합니다.
    
    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken, apiurl"
    ```
    {: codeblock}
    
    명령을 실행한 후 프롬프트가 표시되면 `apiurl`을 `https://<YourManagedServerURL>/e/<environmentID>/api`로 설정하십시오.
    
1. {{site.data.keyword.Bluemix_notm}}에 앱을 푸시한 후 작성한 사용자 제공 서비스를 앱에 바인드하십시오. 예를 들어 다음 명령을 사용하십시오.
    ```
    ibmcloud cf bs myApp dynatrace-service
    ```
    {: codeblock}

    **참고**: 서비스를 바인드한 후 애플리케이션을 다시 스테이징해야 합니다.

   또는 사용자 제공 서비스 이름을 앱의 `manifest.yml` 파일에 있는 `service` 섹션에 추가하여 서비스를 앱에 바인드할 수 있습니다.
   ```yaml
   ---
    applications:
    - path: .
      memory: 256M
      instances: 1
      name: myApp
      host: myApp
      disk_quota: 1024M
    services:
      - dynatrace-service
   ```
   {: codeblock}
