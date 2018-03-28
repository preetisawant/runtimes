---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}

{{site.data.keyword.Bluemix}}의 PHP 런타임은 php_buildpack을 통해 제공됩니다.

php_buildpack은 PHP 앱을 위한 완전한 런타임 환경을
제공합니다.
{: shortdesc}

php_buildpack은 다음과 같은 조건에서 사용됩니다.
* 앱에 composer.json 파일이 있는 경우. 또는
* 앱에 *.php 파일이 있는 경우. 또는
* 앱이 [options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html) 파일에 ${WEBDIR} 변수를 정의하고, 해당 변수가 앱에 있는 기존 디렉토리로 설정된 경우.

## 스타터 애플리케이션
{: #starter_application}

{{site.data.keyword.Bluemix}}는 PHP 스타터 애플리케이션을 제공합니다.  PHP 스타터 애플리케이션은 앱에 사용할 수 있는 템플리트를 제공하는 단순한 PHP 앱입니다. 스타터 앱을 사용하여 시험해 볼 수 있으며 {{site.data.keyword.Bluemix}} 환경을 변경하고 변경사항을 푸시할 수
있습니다.  스타터 애플리케이션 사용에 대한 도움말은 [스타터 애플리케이션 사용](/docs/cfapps/starter_app_usage.html)을 참조하십시오.

## 애플리케이션의 모든 페이지에서 HTTPS 강제 실행
{: #enforce_https}

Apache를 사용하여 {{site.data.keyword.Bluemix_notm}}를 실행할 때 애플리케이션의 모든 페이지에서 HTTP 대신 HTTPS를 강제 실행하려면 ".htaccess" 파일에 대해 다음과 같이 변경해야 합니다.  이 규칙은 {{site.data.keyword.Bluemix_notm}}에서 실행 중인 경우에만 HTTPS를 사용하여 작성되지 않은 요청에 적용됩니다.

```
RewriteCond %{HTTP:X-Forwarded-Proto} !=https [NC]
RewriteCond %{ENV:BLUEMIX_REGION} !^$
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

## 런타임 버전
{: #runtime_versions}

composer.json 파일에서 앱이 사용할 PHP 버전을 지정할 수 있습니다. 예를 들어, 다음과 같습니다.

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
자세한 정보는 [Composer Package links ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://getcomposer.org/doc/04-schema.md#package-links)를 참조하십시오.

버전이 지정되지 않은 경우 기본적으로 버전 5.6.31이 선택됩니다.

### 사용 가능한 버전:
{: #available_versions}

다음 PHP 버전은 현재
{{site.data.keyword.Bluemix}}에 설치된 [PHP 빌드팩](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.27)에서
사용 가능합니다.

* 5.6.30
* 5.6.31
* 7.0.20
* 7.0.21
* 7.1.6
* 7.1.7

나열되지 않은 PHP 버전이 애플리케이션에 필요한 경우
외부
[PHP 빌드팩](https://github.com/cloudfoundry/php-buildpack.git)을
사용하여 애플리케이션을 배치할 수 있습니다.

# 관련 링크
{: #rellinks notoc}
## 튜토리얼 및 샘플
{: #samples notoc}
* [REST API 빌드 및 배치](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [모바일 친화 칼로리 카운터 빌드 및 배치](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## 일반
{: #general notoc}
* [PHP에 대한 Cloud Foundry 빌드팩](https://github.com/cloudfoundry/php-buildpack.git)
