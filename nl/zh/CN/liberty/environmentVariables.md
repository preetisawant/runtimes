---

copyright:
  years: 2015, 2019
lastupdated: "2018-02-01"
subcollection: "liberty"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 环境变量
{: #environment_variables}

Liberty for Java 支持的环境变量。

<table>
<tr>
<th align="left">环境变量名</th>
<th align="left">描述</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>启用[应用程序管理实用程序](/docs/runtimes-common/app_mng.html)</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>安装[应用程序管理实用程序](/docs/runtimes-common/app_mng.html)</td>
</tr>

<tr>
<td>IBM_LIBERTY_MONTHLY</td>
<td>启用 [Liberty 每月发行版运行时](/docs/runtimes/liberty/usingMonthlyRuntime.html)</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>设置 [Java 选项](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>配置 [Dynatrace 代理程序位置信息](/docs/runtimes/liberty/monitoring/dynatrace.html#configuring_liberty_app)</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>配置 [IBM JRE 版本](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>配置各种 Liberty 运行时选项，包括[用于 WAR 或 EAR 文件的功能](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>配置 [OpenJDK 版本](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION</td>
<td>禁用 [Spring 自动重新配置框架](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/framework-spring_auto_reconfiguration.md)。要禁用，请将值设置为 enabled: false。</td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>设置 buildpack 的日志记录级别。可能的值：<b>DEBUG</b>、<b>INFO</b>（缺省值）、<b>WARN</b>、<b>ERROR</b> 或 <b>FATAL</b></td>
</tr>

<tr>
<td>JVM</td>
<td>选择 [JRE 类型](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>设置 [JVM 自变量](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[覆盖服务配置](/docs/runtimes/liberty/autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>设置代理服务器信息</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>设置代理服务器信息</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>禁用服务[自动配置](/docs/runtimes/liberty/autoConfig.html#opting_out)。</td>
</tr>
</table>
{: caption="表 1. 可用于 Liberty for Java 的环境变量" caption-side="top"}

## Liberty for Java buildpack 中的禁用属性

Liberty buildpack 会自动禁用一些属性。您无法覆盖这些属性。下面列出了会被禁用的环境变量和属性。

### 禁用属性表

<table>
<tr>
<th>禁用的属性</th>
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
{: caption="表 1. Liberty for Java 禁用的属性" caption-side="top"}
