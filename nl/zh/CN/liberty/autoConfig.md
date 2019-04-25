---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 配置绑定的服务
{: #auto_config}

您可以将各种服务绑定到 Liberty for Java 应用程序。可以是容器管理服务和/或应用程序管理服务，具体取决于开发者的需要。

应用程序管理的服务是完全由应用程序管理而无需 Liberty 任何协助的服务。应用程序通常会读取 VCAP_SERVICES 来获取有关绑定服务的信息，并会直接访问服务。应用程序提供所有必要的客户机访问代码。完全不依赖于 Liberty 功能或 `server.xml` 文件配置。Liberty buildpack 自动配置不会应用于此类型的服务。

容器管理的服务是由 Liberty 运行时管理的服务。在一些情况下，应用程序可能会在 JNDI 中查找绑定服务，而在另一些情况下，服务由 Liberty 本身直接使用。Liberty buildpack 会读取 VCAP_SERVICES 来获取有关绑定服务的信息。对于每个容器管理的服务，该 buildpack 会执行三个功能。

* 为绑定服务生成[云变量](/docs/runtimes/liberty/optionsForPushing.html#accessing_info_of_bound_services)。
* 安装 Liberty 功能和为了访问绑定服务所需的客户机访问代码。
* 生成或更新服务所需的 `server.xml` 文件节。

此过程称为自动配置。

Liberty buildpack 提供以下服务类型的自动配置：

* [{{site.data.keyword.autoscaling}}](/docs/services/Auto-Scaling/index.html#autoscaling)
* [ClearDB MySQL Database ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.cleardb.com/developers)
* [{{site.data.keyword.cloudant}}](/docs/services/Cloudant/index.html#Cloudant)
* [{{site.data.keyword.composeForMongoDB}}](/docs/services/ComposeForMongoDB/index.html)
* [{{site.data.keyword.composeForMySQL}}](/docs/services/ComposeForMySQL/index.html)
* [{{site.data.keyword.composeForPostgreSQL}}](/docs/services/ComposeForPostgreSQL/index.html)
* [{{site.data.keyword.dashdbshort}}](/docs/services/dashDB/index.html#dashDB)
* [ElephantSQL](/docs/services/ElephantSQL/index.html)
* [{{site.data.keyword.ssoshort}}](/docs/services/SingleSignOn/index.html#sso_gettingstarted)

Compose 服务可以是容器管理的服务，也可以是应用程序管理的服务。缺省情况下，Liberty buildpack 假定这些服务是容器管理的服务，并自动对其进行配置。如果希望应用程序来管理服务，那么可以通过设置 `services_autoconfig_excludes` 环境变量选择退出服务自动配置。有关更多信息，请参阅[选择退出服务自动配置](/docs/runtimes/liberty/autoConfig.html#opting_out)。

## 安装 Liberty 功能和客户机访问代码
{: #installation_of_liberty_features}

绑定到容器管理的服务时，服务可能需要在 `server.xml` 文件的 `featureManager` 节中配置 Liberty 功能。Liberty buildpack 会更新 `featureManager` 节，并安装所需的支持二进制文件。如果服务需要客户机驱动程序 JAR 文件，那么会将这些文件下载到 Liberty 安装中熟知的位置。

请参阅[选择退出服务自动配置](#opting_out)部分，以了解有关绑定的服务类型的更多详细信息。

## 生成或更新 server.xml 配置节
{: #generating_or_updating_serverxml}

推送独立应用程序时，Liberty buildpack 可以自动生成或更新 `server.xml` 文件中的配置节，具体取决于应用程序绑定到服务的方式以及是否存在现有 `server.xml` 文件。

向 {{site.data.keyword.Bluemix_notm}} 推送独立应用程序时，Liberty buildpack 会生成 `server.xml` 配置节，如[用于推送 Liberty 应用程序的选项](/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing)中所述。

推送独立应用程序并绑定到容器管理的服务时，Liberty buildpack 会为绑定服务生成必要的 `server.xml` 节。

提供 `server.xml` 文件并绑定到容器管理的服务时，Liberty buildpack 将生成或更新配置节。

* 如果提供的 `server.xml` 文件不包含针对绑定服务的配置节，那么 Liberty 将为绑定服务生成配置。
* 如果提供的 `server.xml` 文件包含针对绑定服务的配置节，那么 Liberty 将更新绑定服务的配置。

请参阅绑定服务类型的文档，以获取更多详细信息。

## 选择退出服务自动配置
{: #opting_out}

在某些情况下，您可能不希望 Liberty buildpack 自动配置已绑定的服务。请考虑以下场景。

* 我的应用程序使用的是 *dashDB*，但我希望应用程序直接管理数据库的连接。应用程序包含必要的客户机驱动程序 JAR 文件。我不希望 Liberty buildpack 自动配置 *dashDB* 服务。
* 我提供了 `server.xml` 文件，并且已为 *cloudant* 实例提供配置节，因为我需要非标准数据源配置。我不希望 Liberty buildpack 更新 `server.xml` 文件，但仍需要 Liberty buildpack 确保安装相应的支持软件。

要选择退出自动服务配置，请使用 services_autoconfig_excludes 环境变量。可以将此环境变量包含在 manifest.yml 中，或者使用 {{site.data.keyword.Bluemix_notm}} 客户机对其进行设置。

可以按每种服务类型来选择退出自动配置服务。您可以选择完全退出（如 *dashDB* 场景中那样），也可以选择仅退出 `server.xml` 文件配置更新（如 *cloudant* 场景中那样）。为 services_autoconfig_excludes 环境变量指定的值是字符串，如下所示。

* 字符串可以包含一个或多个服务的选择退出规范。
* 特定服务的选择退出规范是 service_type=option，其中：
  * service_type 是服务的标签，如 VCAP_SERVICES 中显示。
  * option 是 `all` 或 `config`。
* 如果字符串包含多个服务的选择退出规范，那么必须使用单个空格字符分隔各个选择退出规范。

请参阅 `services_autoconfig_excludes` 字符串语法的以下示例：

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type (service label as it appears in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: codeblock}

**重要信息**：您指定的服务类型必须与 VCAP_SERVICES 环境变量中所示的服务标签相匹配。不允许使用空格。
**重要信息**：`<service_type_specification>`. 只允许使用空格来分隔多个 `<service_type_specification>` 实例。

使用 **all** 选项可选择退出服务的所有自动配置操作，如上面的 *dashDB* 场景中那样。使用 **config** 选项可仅选择退出配置更新操作，如上面的 *cloudant* 场景中那样。

下面是 `manifest.yml` 文件中针对 *dashDB* 和 *cloudant* 场景的样本选择退出规范。

```
    env:
      services_autoconfig_excludes: dashDB=all

    env:
      services_autoconfig_excludes: cloudant=config

    env:
      services_autoconfig_excludes: cloudant=config dashDB=all
```
{: codeblock}

下面是如何使用命令行界面为应用程序 `myapp` 设置 `services_autoconfig_excludes` 环境变量的示例。

```
    ibmcloud cf set-env myapp services_autoconfig_excludes cloudant=config
    ibmcloud cf set-env myapp services_autoconfig_excludes "cloudant=config dashDB=all"
```
{: codeblock}

要查找 VCAP_SERVICES 中某个服务的 *label*，请发出类似于以下示例的命令：

```
    ibmcloud cf env myapp
```
{: codeblock}

输出包含类似于以下内容的文本，在其中可以看到值为 `elephantsql` 的 **label** 字段：

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

## 覆盖服务配置
{: #override_service_config}

在某些情况下，您可能希望覆盖针对自动配置所生成的服务的缺省配置。
可以使用 **LBP_SERVICE_CONFIG_xxxx** 环境变量来覆盖服务配置。有关完整的环境变量名称和用于覆盖这些变量的示例语法，请参阅以下各表。例如，要覆盖 *elephantSQL* 服务的缺省版本，并将其设置为 V8.3.4.+，请发出如下所示的命令：

```
    ibmcloud cf set-env myapp LBP_SERVICE_CONFIG_POSTGRESQL "{driver: { version: 8.3.4.+ }}"
```
{: codeblock}

下表显示 **service_type** 到 **LBP_SERVICE_CONFIG_xxxx** 环境变量名称的映射。

<table>
<tr>
<th align="left">服务类型</th>
<th align="left">环境变量名</th>
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


下表显示用于覆盖一些服务配置选项的语法：

<table>
<tr>
<th align="left">环境变量名</th>
<th align="left">配置语法</th>
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
