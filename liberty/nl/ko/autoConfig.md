---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 바인드된 서비스 구성
{: #auto_config}

다양한 서비스를 Liberty for Java 애플리케이션에 바인드할 수 있습니다. 개발자에게 필요한 기능에 따라 서비스는 컨테이너 관리형, 애플리케이션 관리형 또는 두 형태 모두로 제공됩니다.

애플리케이션 관리형 서비스는 Liberty의 지원 없이 애플리케이션에서 전적으로 관리하는 서비스입니다. 일반적으로 VCAP_SERVICES를 읽어 바인드된 서비스에 대한 정보를 가져오고 서비스에 직접 액세스합니다. 필요한 모든 클라이언트 액세스 코드가 제공됩니다. Liberty 기능 또는 `server.xml` 파일 구성에 종속되지 않습니다. 이 유형의 서비스에는 Liberty 빌드팩 자동 구성이 적용되지 않습니다.

컨테이너 관리 서비스는 Liberty 런타임에 의해 관리되는 서비스입니다. 경우에 따라 애플리케이션이 JNDI에서 바인드된 서비스를 찾을 때도 있고, 서비스가 Liberty 자체에 바로 사용되는 때도 있습니다. Liberty 빌드팩은 VCAP_SERVICES를 읽어 바인드된 서비스에 대한 정보를 가져옵니다. 각 컨테이너 관리 서비스에 대해 빌드팩은 다음 세 가지 기능을 수행합니다.

* 바인딩된 서비스의 [클라우드 변수](optionsForPushing.html#accessing_info_of_bound_services)를 생성합니다.
* 바인드된 서비스에 액세스하는 데 필요한 클라이언트 액세스 코드 및 Liberty 기능을 설치합니다.
* 서비스에 필요한 `server.xml` 파일 스탠자를 생성하거나 업데이트합니다.

이 프로세스를 자동 구성이라고 합니다.

Liberty 빌드팩은 다음 서비스 유형에 대해 자동 구성을 제공합니다.

* [{{site.data.keyword.autoscaling}}](/docs/services/Auto-Scaling/index.html#autoscaling)
* [ClearDB MySQL Database ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.cleardb.com/developers)
* [{{site.data.keyword.cloudant}}](/docs/services/Cloudant/index.html#Cloudant)
* [{{site.data.keyword.composeForMongoDB}}](/docs/services/ComposeForMongoDB/index.html)
* [{{site.data.keyword.composeForMySQL}}](/docs/services/ComposeForMySQL/index.html)
* [{{site.data.keyword.composeForPostgreSQL}}](/docs/services/ComposeForPostgreSQL/index.html)
* [{{site.data.keyword.dashdbshort}}](/docs/services/dashDB/index.html#dashDB)
* [ElephantSQL](/docs/services/ElephantSQL/index.html)
* [{{site.data.keyword.ssoshort}}](/docs/services/SingleSignOn/index.html#sso_gettingstarted)

Compose 서비스는 컨테이너 관리형 또는 애플리케이션 관리형 중 하나일 수 있습니다. 기본적으로, Liberty 빌드팩은 이러한 서비스가 컨테이너 관리형이라고 가정하며 이를 자동으로 구성합니다. 애플리케이션이 서비스를 관리하게
하려면 `services_autoconfig_excludes` 환경 변수를 설정하여
서비스에 대한 자동 구성을 사용하지 않습니다. 자세한 정보는 [서비스 자동 구성 사용하지 않음](autoConfig.html#opting_out)을 참조하십시오.

## Liberty 기능 및 클라이언트 액세스 코드 설치
{: #installation_of_liberty_features}

컨테이너 관리 서비스에 바인드하는 경우, 서비스가 `server.xml` 파일의 `featureManager` 스탠자에 Liberty 기능을 구성해야 할 수 있습니다. Liberty 빌드팩은 `featureManager` 스탠자를 업데이트하고 필요한 지원 바이너리 파일을 설치합니다. 서비스에 클라이언트 드라이버 JAR 파일이 필요하면 설치된 Liberty의 알려진 위치에 이 파일이 다운로드됩니다.

바인드된 서비스 유형에 대한 자세한 정보는 [서비스 자동 구성 사용하지 않음](#opting_out) 섹션을 참조하십시오.

## server.xml 구성 스탠자 생성 또는 업데이트
{: #generating_or_updating_serverxml}

Liberty 빌드팩은 애플리케이션이 서비스에 바인드된 방법과 사용자에게 기존 `server.xml` 파일이 있는지 여부에 따라 사용자가 독립형 애플리케이션을 푸시할 때 `server.xml` 파일의 구성 스탠자를 자동으로 생성하거나 업데이트할 수 있습니다.

독립형 애플리케이션을 푸시하는 경우, Liberty 빌드팩은 [Liberty 애플리케이션 푸시를 위한 옵션](optionsForPushing.html#options_for_pushing)에 설명된 대로 `server.xml` 구성 스탠자를 {{site.data.keyword.Bluemix_notm}}에 생성합니다.

독립형 애플리케이션을 푸시하고 컨테이너 관리 서비스에 바인드하면 Liberty 빌드팩에서 바인드된 서비스에 필요한 `server.xml` 스탠자를 생성합니다.

`server.xml` 파일을 제공하고 이를 컨테이너 관리 서비스에 바인드하는 경우, Liberty 빌드팩은 구성 스탠자를 생성하거나 업데이트합니다.

* 제공된 `server.xml` 파일에 바인드된 서비스에 대한 구성 스탠자가 포함되지 않은 경우, Liberty는 바인드된 서비스에 대한 구성을 생성합니다.
* 제공된 `server.xml` 파일에 바인드된 서비스에 대한 구성 스탠자가 포함된 경우, Liberty는 바인드된 서비스에 대한 구성을 업데이트합니다.

자세한 정보는 바인드된 서비스 유형과 관련된 문서를 참조하십시오.

## 서비스 자동 구성 사용 안함
{: #opting_out}

Liberty 빌드팩을 통해 바인드된 서비스를 자동으로 구성하지 않으려는 경우가 있습니다. 다음 시나리오를 고려하십시오.

* 내 애플리케이션이 *dashDB*를 사용하지만, 애플리케이션이 데이터베이스에 대한 연결을 직접 관리하도록 하고 싶습니다. 애플리케이션에 필요한 클라이언트 드라이버 JAR 파일이 들어 있습니다. Liberty 빌드팩이 *dashDB* 서비스를 자동으로 구성하는 것을 원하지 않습니다.
* 표준이 아닌 데이터 소스 구성이 필요하므로, `server.xml` 파일을 제공 중이며 *cloudant* 인스턴스에 대한 구성 스탠자를 제공했습니다. Liberty 빌드팩을 통해 내 `server.xml` 파일이 업데이트되는 것을 원하지 않지만, 올바른 지원 소프트웨어가 설치되어 있는지 확인하기 위해 Liberty 빌드팩이 계속 필요합니다.

자동 서비스 구성을 사용하지 않으려면 services_autoconfig_excludes 환경 변수를 사용하십시오. 이 환경 변수를 manifest.yml에 포함하거나 {{site.data.keyword.Bluemix_notm}} 클라이언트를 사용하여 설정합니다.

서비스 자동 구성은 서비스 유형별로 사용하지 않을 수 있습니다. 완전히 사용하지 않거나(*dashDB* 시나리오에서와 같이) `server.xml` 파일 구성 업데이트만 사용하지 않도록(*cloudant* 시나리오에서와 같이) 선택할 수 있습니다. services_autoconfig_excludes 환경 변수에 대해 지정된 값은 아래에 표시된 대로 문자열입니다.

* 문자열에는 하나 이상의 서비스에 대한 옵트 아웃 명세가 포함될 수 있습니다.
* 특정 서비스의 옵트 아웃 명세는 service_type=option입니다. 여기서,
  * service_type은 VCAP_SERVICES에 표시된 서비스의 레이블입니다.
  * 옵션은 `all` 또는 `config`입니다. 
* 문자열에 두 개 이상 서비스에 대한 옵트 아웃 명세가 포함되어 있는 경우, 공백 문자 하나를 사용해 개별 옵트 아웃 명세를 구분해야 합니다.

`services_autoconfig_excludes` 문자열 문법의 다음 예를 참조하십시오.

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type (service label as it appears in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: codeblock}

**중요**: 사용자가 지정한 서비스 유형이 VCAP_SERVICES 환경 변수에 표시된 서비스 레이블과 일치해야 합니다. 공백은 허용되지 않습니다.
**중요**: `<service_type_specification>`에 공백을 사용할 수 없습니다. 단, 여러 개의 `<service_type_specification>` 인스턴스를 구분하는 목적으로만 유일하게 공백을 사용할 수 있습니다.

위의 *dashDB* 시나리오에서와 같이 서비스에 대한 자동 구성 조치를 모두 사용하지 않으려면 **all** 옵션을 사용하십시오. 위의 *cloudant* 시나리오에서와 같이 구성 업데이트 조치만 사용하지 않으려면 **config** 옵션을 사용하십시오.

다음은 *dashDB* 및 *cloudant* 시나리오에 대한 `manifest.yml` 파일의 샘플 옵트 아웃 명세입니다.

```
    env:
      services_autoconfig_excludes: dashDB=all

    env:
      services_autoconfig_excludes: cloudant=config

    env:
      services_autoconfig_excludes: cloudant=config dashDB=all
```
{: codeblock}

다음은 명령행 인터페이스를 사용하여 애플리케이션 `myapp`에 `services_autoconfig_excludes` 환경 변수를 설정하는 방법의 예입니다.

```
    ibmcloud cf set-env myapp services_autoconfig_excludes cloudant=config
    ibmcloud cf set-env myapp services_autoconfig_excludes "cloudant=config dashDB=all"
```
{: codeblock}

VCAP_SERVICES의 서비스에 대한 *label*을 찾으려면 다음 예와 같은 명령을 실행하십시오.

```
    ibmcloud cf env myapp
```
{: codeblock}

출력에는 다음과 유사한 텍스트가 포함되며, 여기서 `elephantsql` 값의 **label** 필드를 볼 수 있습니다.

```
   "elephantsql": [
   {
      "credentials": {
      "max_conns": "5",
      "uri":      "..."
   },
   "label": "elephantsql",

```
{: codeblock}

## 서비스 구성 대체
{: #override_service_config}

경우에 따라서는 자동 구성으로 생성된 서비스의 기본 구성을 대체하고자 할 수 있습니다.
**LBP_SERVICE_CONFIG_xxxx** 환경 변수를 사용하여 서비스 구성을 대체할 수 있습니다. 전체 환경 변수 이름 및 이를 대체하기 위한 예제 구문은 다음 표를 참조하십시오.  예를 들어, *elephantSQL* 서비스의 기본 버전을 대체하고 이를 8.3.4.+ 버전으로 설정하려면 다음과 같은 명령을 실행하십시오.

```
    ibmcloud cf set-env myapp LBP_SERVICE_CONFIG_POSTGRESQL "{driver: { version: 8.3.4.+ }}"
```
{: codeblock}

이 표는 **service_type**에서 **LBP_SERVICE_CONFIG_xxxx** 환경 변수 이름으로의 맵핑을 보여줍니다.

<table>
<tr>
<th align="left">service_type</th>
<th align="left">환경 변수 이름</th>
</tr>

<tr>
<td>Auto-Scaling</td>
<td>LBP_SERVICE_CONFIG_AUTO-SCALING</td>
</tr>

<tr>
<td>cleardb</td>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
</tr>

<tr>
<td>cloudantNoSQLDB</td>
<td>LBP_SERVICE_CONFIG_CLOUDANTNOSQLDB</td>
</tr>

<tr>
<td>compose-for-mongodb</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MONGO</td>
</tr>

<tr>
<td>compose-for-mysql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
</tr>

<tr>
<td>compose-for-postgresql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
</tr>

<tr>
<td>elephantsql</td>
<td>LBP_SERVICE_CONFIG_POSTGRESQL</td>
</tr>

<tr>
<td>SingleSignOn</td>
<td>LBP_SERVICE_CONFIG_SINGLESIGNON</td>
</tr>
</table>


다음 표에 몇몇 서비스 구성 대체 옵션의 구문이 표시되어 있습니다.

<table>
<tr>
<th align="left">환경 변수 이름</th>
<th align="left">구성 구문</th>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>
</table>
