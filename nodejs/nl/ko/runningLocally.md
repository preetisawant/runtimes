---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 로컬에서 Node.js 애플리케이션 실행
{: #hints}

{{site.data.keyword.Bluemix}}에서 실행할 때 충돌을 일으키지 않고 로컬에서 Node.js 애플리케이션을 실행하도록 포트 번호를 설정하십시오.
{: shortdesc}

{{site.data.keyword.Bluemix_notm}}에서 애플리케이션을 실행 중인 경우 Cloud Foundry에서 PORT 환경 변수를 할당합니다. 그러나 애플리케이션이 로컬에서 실행 중인 경우 PORT가 정의되지 않으므로 애플리케이션의 포트를 정의할 수 있습니다. 충돌을 방지하려면 {{site.data.keyword.Bluemix_notm}}에서 사용하는 포트와 다르게 앱이 로컬에서 청취하는 포트를 정의하십시오.

**js** 파일의 다음 예에서 **3000**을 포트 번호로 사용합니다. **3000**을 사용하면 애플리케이션을 테스트 용도로 로컬에서 실행하고 {{site.data.keyword.Bluemix_notm}}에서는 변경 없이 실행할 수 있습니다.

```
var port = (process.env.PORT || 3000);
```
{: codeblock}
