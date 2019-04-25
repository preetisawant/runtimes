---

copyright:
  years: 2016, 2018
lastupdated: "2018-06-27"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 在 {{site.data.keyword.cloud_notm}} 中使用 Dynatrace 监视 Liberty
{: #using_dynatrace}

Dynatrace 是第三方服务，它提供对应用程序的监视。您可以将 Dynatrace 与 Liberty 应用程序集成，但 IBM 不提供对第三方服务的支持。有关更多信息，请参阅[第三方服务](/docs/runtimes-common/buildpackSupport.html#third-party)。

有关 Dynatrace 及其许可的更多信息，请参阅 [Dynatrace Application Monitoring ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://www.dynatrace.com/en/products/application-monitoring.html)。

将 Liberty 应用程序配置为使用 Dynatrace 时，缺省行为是 Liberty 运行时将从 Dynatrace 站点获取 Dynatrace 代理程序 `.jar` 文件，并会在运行应用程序时运行该 Dynatrace 代理程序。在缺省行为下，使用 Dynatrace 所需的最低配置为创建指向 Dynatrace 收集器的用户提供服务。

## 创建指向 Dynatrace 收集器的用户提供服务

首先，您需要设置 Dynatrace 收集器。然后，还必须创建用户提供的服务来传递 Dynatrace 代理程序的信息，以便与 Dynatrace 收集器进行连接。要更好地理解 Dynatrace 组件之间的关系，请参阅 [Dynatrace Architecture ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://community.dynatrace.com/community/display/DOCDT65/Architecture)。

1. 设置 Dynatrace 收集器。
  * 有关下载和设置 Dynatrace 收集器的指示信息，请参阅 [Dynatrace 社区 Web 站点 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace)。
  * 确保从设置收集器的位置可以访问随 {{site.data.keyword.Bluemix_notm}} 中应用程序运行的 Dynatrace 代理程序。
2. 创建指向运行中 Dynatrace 收集器的用户提供服务。

  **注**：用户提供的服务的名称必须包含字符串 **dynatrace**。将忽略大小写。例如，使用以下命令，其中 **my-dynatrace-collector** 包含 **dynatrace**：
  ```
  ibmcloud cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
  ```
  {: codeblock}

    在此示例中，my-dynatrace-collector 是为服务指定的名称，DynatraceCollectorIPaddress 是已配置的 Dynatrace 收集器的 IP 地址，profile 是与此受监视应用程序关联的可选 Dynatrace 概要文件名称。缺省概要文件值为 Monitoring。可以指定可选参数，如以下示例中所示。


    ```
ibmcloud cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                      "options" : {"dynatrace-parameter-1": "value",
                                   "dynatrace-parameter-2": "value"}}'
    ```
    {: codeblock}

    有关可用选项的更多信息，请参阅 Dynatrace 社区 Web 站点上 [Agent Configuration 的 _Agent Settings_ 部分 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://community.dynatrace.com/community/display/DOCDT65/Set+up+Agents)。例如，使用 exclude 选项，可以排除某些类使之不受 Dynatrace 监视。有关配置用户提供的服务的更多详细信息，请参阅 [Dynatrace Agent Framework ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md)。

3. 将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 后，将您创建的用户提供的服务绑定到应用程序。例如，使用以下命令：
  ```
  ibmcloud cf bs myApp my-dynatrace-collector
  ```
  {: codeblock}

    **注**：绑定服务后，必须重新编译打包应用程序。

## 可选配置
{: #optional_configuration}

您可以选择自行获取并托管 Dynatrace 代理程序 `.jar` 文件。在此情况下，需要执行以下额外的配置步骤。
1. 获取并托管 Dynatrace 代理程序 `.jar` 文件，以便 Liberty buildpack 可以下载该文件。
2. 配置 Liberty 应用程序，以便其可以下载 Dynatrace 代理程序。

### 托管 Dynatrace 代理程序
{: #hosting_dynatrace_agent}
必须在 Web 服务器上托管 Dynatrace 代理程序，并且必须使 Liberty buildpack 能够从该服务器下载代理程序 `.jar` 文件。必须为该服务器配置一个 `index.yml` 文件，用于指定有关代理程序 `.jar` 文件的详细信息。完成下面的步骤以设置 Dynatrace 代理程序：
  1. 下载 Dynatrace 代理程序 `.jar` 文件。有关下载 Dynatrace 代理程序 `.jar` 文件的指示信息，请参阅 Dynatrace 社区 Web 站点上的 [Dynatrace Server Platform Installers ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace)。用于在 {{site.data.keyword.Bluemix_notm}} 上运行的相应代理程序 `.jar` 文件为 **dynatrace-agent-unix.jar** V**6.+**。
  2. 在 Liberty buildpack 可以下载代理程序 `.jar` 文件的位置托管该文件。可以使用任一可用的服务器工具在 {{site.data.keyword.Bluemix_notm}} 本身上托管该 jar 文件，也可以在某些公共可用的位置进行托管。
     * 确保在托管位置提供 `index.yml` 文件。`index.yml` 文件必须包含由以下各项组成的一个条目：代理程序 `.jar` 文件的版本标识，后跟一个冒号和该代理程序 `.jar` 文件所在位置的完整 URL。例如：

            ---
               6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
            {: codeblock}

     * **dynatrace-agent-6.3.0-unix.jar** 文件必须在 `index.yml` 文件中指定的位置提供。`.jar` 文件和 `index.yml` 可以位于同一目录。

### 配置 Liberty 应用程序
{: #configuring_liberty_app}

必须将要监视的 Liberty 应用程序配置为可找到先前设置的托管代理程序 `.jar` 文件的服务器。可以使用 **JBP_CONFIG_DYNATRACEAPPMONAGENT** 环境变量来配置应用程序。**JBP_CONFIG_DYNATRACEAPPMONAGENT** 环境变量会通知 buildpack 从什么位置下载 Dynatrace 代理程序。要设置该环境变量，请完成以下步骤：

1. 设置变量 **JBP_CONFIG_DYNATRACEAPPMONAGENT**，使其具有值 *"repository_root: URL_of_server_hosting_index.yml"*。例如，推送应用程序后，发出以下命令：


        ibmcloud cf se myApp JBP_CONFIG_DYNATRACEAPPMONAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
        {: codeblock}

    在此示例中，*my-dynatrace-agent-host.mybluemix.net* 是先前配置的服务器托管的 `index.yml` 文件的 URL。

2. 设置该环境变量后，对应用程序重新编译打包。检查编译打包日志中是否有消息指示从托管代理程序的服务器成功下载了 Dynatrace 代理程序。例如：
```
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
```
{: codeblock}
