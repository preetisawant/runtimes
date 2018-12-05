---

copyright:
  years: 2018
lastupdated: "2018-11-09"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# 후크를 사용하여 서드파티 서비스 통합
{: #hooks}

후크를 사용하여 SDK for Node.js 빌드팩의 서드파티 서비스를 쉽게 통합할 수 있습니다. IBM은 통합하는 서드파티 서비스에 대한 지원을 제공하지 않습니다. 지원에 대한 자세한 정보는 [서드파티 서비스](../common/buildpackSupport.html#third-party)를 참조하십시오.

SDK for Node.js 빌드팩에는 Dynatrace 후크가 포함됩니다. Dynatrace는 Node.js 애플리케이션의 애플리케이션 모니터링을 사용으로 설정합니다. [Dynatrace 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")]( https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/application-only/deploy-oneagent-on-cloud-foundry-for-application-only-monitoring/){: new_window}에서 빌드팩의 Dynatrace 후크 사용에 대해 자세히 알아보십시오.


서드파티 문서의 지시사항을 따를 때 `cf` 대신 `ibmcloud cf` 명령을 사용하여 {{site.data.keyword.Bluemix_notm}} 빌드팩에 대한 명령을 실행하십시오.
{: tip}
