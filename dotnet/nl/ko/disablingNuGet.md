---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# NuGet 패키지 캐시 사용 안함
{: #disabling_the_nuget_package_cache}

일부 상황에서 애플리케이션의 NuGet 패키지 캐시를 지워야 할 수 있습니다.  이렇게 하면 캐시된 기존 NuGet 패키지가 지워지고 빌드팩이 새 패키지를 캐시하지 않게 됩니다.

{{site.data.keyword.Bluemix_notm}} CLI를 통해 `CACHE_NUGET_PACKAGES` 환경 변수를 `false`로 설정하여 캐시를 지울 수 있습니다.

```shell
  ibmcloud cf set-env <app_name> CACHE_NUGET_PACKAGES false
```
{: codeblock}

또는 애플리케이션 `manifest.yml` 파일에서 `CACHE_NUGET_PACKAGES` 환경 변수를 `false`로 설정할 수 있습니다.

```yml
---
applications:
- name: sample-aspnetcore-app
  memory: 512M
  env:
    CACHE_NUGET_PACKAGES: false
```
{: codeblock}
