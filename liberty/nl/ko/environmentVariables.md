---

copyright:
  years: 2015, 2019
lastupdated: "2018-02-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 환경 변수
{: #environment_variables}

Liberty for Java에서 지원하는 환경 변수

<table>
<tr>
<th align="left">환경 변수 이름</th>
<th align="left">설명</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>[App Management 유틸리티](/docs/runtimes-common/app_mng.html)를 사용으로 설정합니다.</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>[App Management 유틸리티](/docs/runtimes-common/app_mng.html)를 설치합니다.</td>
</tr>

<tr>
<td>IBM_LIBERTY_MONTHLY</td>
<td>[Liberty 월별 릴리스 런타임](/docs/runtimes/liberty/usingMonthlyRuntime.html)을 사용으로 설정합니다. </td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>[Java 옵션](/docs/runtimes/liberty/customizingJRE.html)을 설정합니다.</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>[Dynatrace 에이전트 위치 정보](/docs/runtimes/liberty/monitoring/dynatrace.html#configuring_liberty_app)를 구성합니다.</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>[IBM JRE 버전](/docs/runtimes/liberty/customizingJRE.html)을 구성합니다.</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>[WAR 또는 EAR 파일의 기능](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)을 포함하여 다양한 Liberty 런타임 옵션을 구성합니다.</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>[OpenJDK JRE 버전](/docs/runtimes/liberty/customizingJRE.html)을 구성합니다. </td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>[Spring Auto-Reconfiguration 프레임워크](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/framework-spring_auto_reconfiguration.md)를 사용하지 않습니다. 사용 안함으로 설정하려면 값을 enabled: false로 설정하십시오. </td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>빌드팩의 로깅 레벨을 설정합니다. 가능한 값: <b>DEBUG</b>, <b>INFO</b>(기본값), <b>WARN</b>, <b>ERROR</b> 또는 <b>FATAL</b></td>
</tr>

<tr>
<td>JVM</td>
<td>[JRE 유형](/docs/runtimes/liberty/customizingJRE.html)을 선택합니다.</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>[JVM 인수](/docs/runtimes/liberty/customizingJRE.html)를 설정합니다.</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[서비스 구성을 대체합니다. ](/docs/runtimes/liberty/autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>프록시 서버 정보를 설정합니다.</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>프록시 서버 정보를 설정합니다.</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>[auto-configuration](/docs/runtimes/liberty/autoConfig.html#opting_out) 서비스를 사용 안함으로 설정합니다.</td>
</tr>
</table>
{: caption="표 1. Liberty for Java에 사용 가능한 환경 변수" caption-side="top"}

## Liberty for Java 빌드팩에서 사용 안함으로 설정된 속성

일부 속성은 Liberty 빌드팩에 의해 자동으로 사용 안함으로 설정되며 이를 대체할 수 없습니다. 다음 환경 변수와 속성은 사용 안함으로 설정됩니다.

### 사용 안함으로 설정된 속성 표

<table>
<tr>
<th>사용 안함으로 설정된 속성 </th>
<th>요소</th>
</tr>

<tr>
<td>host</td>
<td>httpEndpoint</td>
</tr>

<tr>
<td>httpPort</td>
<td>httpEndpoint</td>
</tr>

<tr>
<td>trustHostHeaderPort</td>
<td>webContainer</td>
</tr>

<tr>
<td>andextractHostHeaderPort</td>
<td>webContainer</td>
</tr>

<tr>
<td>logDirectory</td>
<td>logging</td>
</tr>

<tr>
<td>consoleLogLevel</td>
<td>logging</td>
</tr>

<tr>
<td>enableWelcomePage</td>
<td>httpDispatcher</td>
</tr>
</table>
{: caption="표 1. Liberty for Java에서 사용 안함으로 설정한 속성" caption-side="top"}
