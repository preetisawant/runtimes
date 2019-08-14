---

copyright:
  years: 2015, 2019
lastupdated: "2018-02-01"
subcollection: "liberty"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 環境變數
{: #environment_variables}

Liberty for Java 支援的環境變數。

<table>
<tr>
<th align="left">環境變數名稱</th>
<th align="left">說明</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>啟用[應用程式管理公用程式](/docs/runtimes-common/app_mng.html)</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>安裝[應用程式管理公用程式](/docs/runtimes-common/app_mng.html)</td>
</tr>

<tr>
<td>IBM_LIBERTY_MONTHLY</td>
<td>啟用 [Liberty 每月版本運行環境](/docs/runtimes/liberty/usingMonthlyRuntime.html)</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>設定 [Java 選項](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>配置 [Dynatrace 代理程式位置資訊](/docs/runtimes/liberty/monitoring/dynatrace.html#configuring_liberty_app)</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>配置 [IBM JRE 版本](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>配置各種 Liberty 運行環境選項，包括 [WAR 檔或 EAR 檔的特性](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>配置 [OpenJDK 版本](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>停用 [Spring Auto-Reconfiguration 架構](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/framework-spring_auto_reconfiguration.md)。若要停用，請將值設為 enabled: false。</td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>設定建置套件的記載層次。可能值：<b>DEBUG</b>、<b>INFO</b>（預設值）、<b>WARN</b>、<b>ERROR</b> 或 <b>FATAL</b></td>
</tr>

<tr>
<td>JVM</td>
<td>選取 [JRE 類型](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>設定 [JVM 引數](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[置換服務配置](/docs/runtimes/liberty/autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>設定 Proxy 伺服器資訊</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>設定 Proxy 伺服器資訊</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>停用服務[自動配置](/docs/runtimes/liberty/autoConfig.html#opting_out)。</td>
</tr>
</table>
{: caption="表 1. Liberty for Java 可用的環境變數" caption-side="top"}

## Liberty for Java 建置套件中已停用的屬性

Liberty 建置套件會自動停用一些您無法置換的屬性。已停用下列環境變數及屬性。

### 已停用的屬性表格

<table>
<tr>
<th>已停用的屬性</th>
<th>元素</th>
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
{: caption="表 1. Liberty for Java 已停用的屬性" caption-side="top"}
