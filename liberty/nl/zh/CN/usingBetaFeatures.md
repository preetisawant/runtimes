---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 Beta 功能
{: #using_beta_features}

Liberty Beta 功能让您可以提早使用未来 Liberty 发行版中可能会包含的新功能和编程模型。大部分 Beta 功能还可以在部署到 {{site.data.keyword.Bluemix}} 的应用程序中使用。

**重要信息**：Beta 功能仅用于开发和测试，而不可用于生产。有关完整的使用条款，请参阅 [Beta 许可协议](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html)。

{{site.data.keyword.Bluemix_notm}} 中可用的 Liberty Beta 功能
<table>
<tr>
<th align="left">功能</th>
</tr>

<tr>
    <tr><td>appSecurity-3.0</tr></td>
    <tr><td>audit-1.0</tr></td>
    <tr><td>beanValidation-2.0</tr></td>
    <tr><td>bluemixLogCollector-1.1</tr></td>
    <tr><td>cdi-2.0</tr></td>
    <tr><td>javaee-8.0</tr></td>
    <tr><td>javaeeClient-8.0</tr></td>
    <tr><td>jaxrs-2.1</tr></td>
    <tr><td>jpa-2.2</tr></td>
    <tr><td>jpaContainer-2.2</tr></td>
    <tr><td>jsf-2.3</tr></td>
    <tr><td>jsfContainer-2.2</tr></td>
    <tr><td>jsonb-1.0</tr></td>
    <tr><td>jsonbContainer-1.0</tr></td>
    <tr><td>jsonp-1.1</tr></td>
    <tr><td>jsonpContainer-1.1</tr></td>
    <tr><td>logstashCollector-1.1</tr></td>
    <tr><td>mpConfig-1.2</tr></td>
    <tr><td>mpOpenAPI-1.0</tr></td>
    <tr><td>mpRestClient-1.0</tr></td>
    <tr><td>opentracing-1.0</tr></td>
    <tr><td>servlet-4.0</tr></td>
    <tr><td>validator-1.0</tr></td>
    <tr><td>webProfile-8.0</tr></td>

</tr>
</table>

要在 {{site.data.keyword.Bluemix_notm}} 中使用 Liberty Beta 功能，您将需要执行以下操作：

1. [部署服务器目录或打包服务器](optionsForPushing.html)，并在 server.xml 文件中启用一个或多个 Beta 功能，如以下示例中所示：
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>mpOpenAPI-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  将 **IBM_LIBERTY_BETA** 环境变量设置为 **true**。此变量会引导 Liberty buildpack 为您的应用程序安装并启用 Beta 功能。例如：
  * 使用 cf 命令行工具：
```
$ cf set-env <yourappname> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * 或者，使用 manifest.yml 文件：
```
env:
          IBM_LIBERTY_BETA: "true"
```

3. 将 **JBP_CONFIG_LIBERTY** 环境变量设置为 **"version: +"**。此变量将启用支持 Beta 功能的 [Liberty 每月运行时](buildpackDefaults.html#liberty_versions)。例如：
  * 使用 cf 命令行工具：
```
$ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * 或者，使用 manifest.yml 文件：
```
env:
          JBP_CONFIG_LIBERTY: "version: +"
```

如果在现有应用程序上启用 Beta 功能，请勿忘记在设置环境变量后重新编译打包应用程序。

{: #codeblock}

# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}
* [Liberty for Java 运行时](index.html)
* [Liberty 概述](https://www.ibm.com/support/knowledgecenter/SSAW57_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/cwlp_about.html)
