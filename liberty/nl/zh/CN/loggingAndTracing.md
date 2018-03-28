---

copyright:
  years: 2015, 2018
lastupdated: "2018-1-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 配置日志记录和跟踪
{: #logging_tracing}

## 日志文件
{: #log_files}

标准 Liberty 日志（例如 `messages.log` 或 `ffdc` 目录）位于 {{site.data.keyword.Bluemix}} 中每个应用程序实例的 `logs` 目录下。这些日志可以从 {{site.data.keyword.Bluemix_notm}} 控制台进行访问，也可以通过 Cloud Foundry CLI 进行访问。例如：

* 要访问应用程序最近的日志，请运行以下命令：

  ```
  cf logs --recent <appname>
  ```
  {: codeblock}


* 要查看应用程序的 `messages.log` 文件，请运行以下命令：

  ```
  cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

日志级别及其他跟踪选项可以通过 Liberty 配置文件进行设置。有关更多信息，请参阅[对 Liberty 进行故障诊断：日志记录和跟踪](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)。

## 使用跟踪和转储功能
{: #using_trace_and_dump}

### 在 {{site.data.keyword.Bluemix_notm}} 控制台中使用跟踪和转储（不推荐）

可以直接从 {{site.data.keyword.Bluemix_notm}} 控制台针对正在运行的应用程序调整 Liberty 跟踪配置。控制台还提供了请求并下载线程和堆转储的功能。为了调整跟踪配置或请求转储，请在 {{site.data.keyword.Bluemix_notm}} 控制台中选择 Liberty 应用程序，然后在导航中选择`运行时`菜单。在`运行时`视图中，选择实例，然后按*跟踪*或*转储*按钮。如果要调整跟踪级别，请参阅 [对 Liberty 进行故障诊断：日志记录和跟踪](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)，以获取有关跟踪规范语法的详细信息。

### 通过 SSH 更改跟踪配置

推送应用程序时，server.xml 文件包含缺省属性 **updateTrigger**（设置为 **polled**）和 **monitorInterval**（设置为 1 分钟）。Liberty 服务器会自动配置为每分钟检查一次 server.xml 的更新。

请参阅[使用 server.xml 推送 Liberty 应用程序](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing)以了解有关使用定制 sever.xml 推送 Liberty 应用程序的选项

请参阅[控制动态更新](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window} 以了解如何在 server.xml 中设置动态更新。

执行以下步骤来更改跟踪配置：

1. SSH 到应用程序

  ```
 cf ssh <appname> [-i instance_index]
  ```
  {: codeblock}

2. 编辑 server.xml 中的 ```<logging traceSpecification="xxxx"/>``` 以设置所需的跟踪规范，例如使用 *vi*：

  ```
vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: codeblock}

注：在重新编译打包或重新启动时，server.xml 更改会丢失，而且此更改仅对 ssh 进入的实例有效。

请参阅 [对 Liberty 进行故障诊断：日志记录和跟踪](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window}，以获取有关跟踪规范语法的详细信息。

### 通过 SSH 触发转储

使用以下命令通过 CF CLI 使用 SSH 功能来触发线程和堆转储：

  ```
 cf ssh <appname> -c "pkill -3 java"
  ```
  {: codeblock}

有关下载生成的转储文件的详细信息，请参阅下面的文档。

## 下载转储文件
{: #download_dumps}

缺省情况下，各种转储文件会放入应用程序容器的 `dumps` 目录中。使用 Cloud Foundry CLI `cf ssh` 来查看和下载转储文件。

* 要查看生成的转储，请运行以下命令：

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* 要下载转储文件，请运行以下命令：

  ```
  cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

还可以使用 `scp` 和其他类似工具来查看并下载转储文件。有关更多信息，请参阅 [Accessing Apps with SSH ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html)。

# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}
* [Liberty 运行时](index.html)
* [Liberty 概述](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
