---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-27"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用自己的 JRE
{: #using_own_jre}

您可以使用自己的 JRE 在 {{site.data.keyword.Bluemix}} 上运行 Liberty 应用程序。liberty-for-java buildpack 将支持 [WebSphere Liberty 支持的运行时](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_restrict.html#rwlp_restrict__rest13)，但无法保证不受支持版本的完全功能。必须完成以下操作，才能使 JRE 可用于应用程序。
* 在 buildpack 可以下载该 JRE 的位置托管该 JRE。
* 托管一个 `index.yml` 文件，该文件用于提供 JRE 的位置。
* 配置应用程序，以使用您的 JRE。

## 托管 JRE 和 `index.yml`
{: #hosting_jre}

必须在 liberty-for-java buildpack 可以从中下载该 JRE 文件的 Web 服务器上托管该文件。可以使用任一可用的服务器工具在 {{site.data.keyword.Bluemix_notm}} 上托管该文件，也可以在公共可用的位置进行托管。该服务器必须配置有一个 `index.yml` 文件，该文件用于指定有关 JRE 文件的详细信息。

要托管 JRE 和 `index.yml` 文件，请完成以下步骤：
  1. 获取 JRE，该 JRE 必须是能够在 UNIX 64 位操作系统上使用的版本，并且必须是 `tar.gz` 文件。
  2. 在 liberty-for-java buildpack 可以从中下载该 JRE 文件的位置中托管该文件。
  3. 在托管位置提供 `index.yml` 文件。`index.yml` 文件中必须包含由以下各项组成的条目：JRE 的版本标识，后跟一个冒号和完整的 JRE 文件位置 URL。
    * 在 `index.yml` 文件中定义 JRE 版本。

    ```
    ---
    jre_version: https://hostingLocation/jreName.tar.gz
    ```
    {: codeblock}

    * 包含 JRE 版本标识和完整的 JRE 文件位置。例如：

    ```
    ---
    1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```
    {: codeblock}

## 配置应用程序
{: #configure_app}

必须在 Liberty 应用程序上设置两个环境变量，以配置 buildpack 使用替代 JRE。设置 **JBP_CONFIG_OPENJDK**，以识别 `index.yml` 文件的位置，并将 **JVM** 环境变量设置为 *openjdk*。有关版本值字符串格式的更多信息，请参阅[版本语法和顺序及通配符 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/util-repositories.md){: new_window} 上的 Cloud Foundry 文档。

**JBP_CONFIG_OPENJDK** 变量的值表示 `index.yml` 文件位置以及从 index.yml 文件中选择的 JRE 版本。

```
'{repository_root: "https://locationToIndexYml", version: version-value}'
```
{: codeblock}

可以发出 `ibmcloud cf se myAPP` 命令来设置 **JBP_CONFIG_OPENJDK** 变量，例如：
```
ibmcloud cf se myApp JBP_CONFIG_OPENJDK '{repository_root: "https://myHostingApp.ng.bluemix.net", version: 1.8.+}'
```
{: codeblock}

*repository_root* URL 的 URL 中不包含 `index.yml`。*repository_root* URL 指向包含 `index.yml` 文件而非文件本身的目录级别。

要设置 JVM 环境变量，请发出以下命令：
```
ibmcloud cf se myApp JVM 'openjdk'
```
{: codeblock}

**注**：设置环境变量后，请重新编译打包应用程序，以使更改生效。

## 确认
{: #confirmation}

要确认 Liberty 使用的是预期 JRE，请检查编译打包日志。查看指示服务器从 `index.yml` 文件所指示位置下载 buildpack 的消息。请参阅以下片段，其为 Liberty 成功使用预期 JRE 时产生的日志输出示例。
```
   -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}
