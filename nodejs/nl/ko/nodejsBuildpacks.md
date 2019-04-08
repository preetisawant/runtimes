---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
subcollection: "Nodejs"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Node.js 빌드팩

{{site.data.keyword.Bluemix}}에서는 여러 버전의 Node.js 빌드팩을 제공합니다.
{: shortdesc}

* {{site.data.keyword.IBM_notm}} 작성 **sdk-for-nodejs** 빌드팩은 {{site.data.keyword.Bluemix_notm}}의 Node.js 애플리케이션에 사용된 기본 빌드팩입니다.
* **nodejs_buildpack**은 Cloud Foundry 커뮤니티에서 제공하는 커뮤니티 빌드팩입니다.

**sdk-for-nodejs** 빌드팩은 {{site.data.keyword.Bluemix_notm}}의 **nodejs_buildpack**에 우선합니다. **sdk-for-nodejs** 빌드팩 대신에 애플리케이션에서 **nodejs_buildpack**을 사용하려면 사용자의 빌드팩을 지정해야 합니다(예: `ibmcloud cf push` 명령에서 `-b` 옵션 사용).

일반적으로 현재 **sdk-for-nodejs** 빌드팩과 이전 레벨 버전이 사용 가능합니다.  사용 가능한 모든 빌드팩을 보려면 `ibmcloud cf buildpacks` 명령을 사용하십시오.  예를 들어, 다음과 같습니다.

```
   ibmcloud cf buildpacks
   Getting buildpacks...

   buildpack                                 position   enabled   locked   filename   

   sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
   nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
   sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}
