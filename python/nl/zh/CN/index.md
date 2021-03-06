---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}

{{site.data.keyword.Bluemix}} 上的 Python 运行时由 python_buildpack 提供支持。python_buildpack 为 Python 2 和 Python 3 应用程序提供了一个完整的运行时环境。
{: shortdesc}

如果您应用程序的根目录中包含 requirements.txt 文件或 setup.py 文件，那么将使用 python_buildpack。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} 提供了 Python 入门模板应用程序。Python 入门模板应用程序是一个简单的 Python 应用程序，它提供了一个可供您的应用程序使用的模板。您可以尝试使用该入门模板应用程序来进行更改并将更改推送到 {{site.data.keyword.Bluemix_notm}} 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](../common/starter_app_usage.html)。

## 运行时版本
{: #runtime_versions}

您可以为您的应用程序指定要使用的 Python 版本，方法是在 runtime.txt 文件中设置 python-versionnumber，该文件位于您应用程序的根目录中。例如：

```
python-3.6.1
```
{: codeblock}

如果未指定版本，缺省情况下会选择 V2.7.14。

### 可用版本：
{: #available_versions}

{{site.data.keyword.Bluemix_notm}} 中当前安装的 [Python buildpack](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.6.11) 内提供了以下 Python 版本：

* 2.7.13
* 2.7.14
* 3.3.6
* 3.3.7
* 3.4.7
* 3.4.8
* 3.5.4
* 3.5.5
* 3.6.3
* 3.6.4

如果您应用程序所需的 Python 版本没有列在上述列表中，那么可以使用外部 [Python buildpack](https://github.com/cloudfoundry/python-buildpack) 来部署应用程序。

# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}
* [用于 Python 的 Cloud Foundry buildpack](https://github.com/cloudfoundry/python-buildpack)
