---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}

{{site.data.keyword.Bluemix}} 上的 Go 运行时由 go_buildpack 提供支持。go_buildpack 为 Go 应用程序提供了一个完整的运行时环境。
{: shortdesc}

如果您的应用程序中包含名为 *.go 的文件，那么将使用 go_buildpack。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} 提供了 Go 入门模板应用程序。Go 入门模板应用程序是一个简单的 Go 应用程序，它提供了一个可供您的应用程序使用的模板。您可以体验该入门模板应用程序，对其进行更改并将更改推送到 {{site.data.keyword.Bluemix_notm}} 环境。请参阅[使用入门模板应用程序](../common/starter_app_usage.html)，以获取有关使用入门模板应用程序的帮助。

## 运行时版本
{: #runtime_versions}

您可以为您的应用程序指定要使用的 Go 版本，方法是在 Godeps/Godeps.json 文件中设置 GoVersion 属性，该文件位于您应用程序的根目录中。例如：

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.8.3",
	"Deps": []
}
```
{: codeblock}
有关更多信息，请参阅 [godep](https://github.com/tools/godep){: new_window}。



如果未指定版本，缺省情况下会选择 V1.8.7。

### 可用版本：
{: #available_versions}

{{site.data.keyword.Bluemix_notm}} 中当前安装的
[Go buildpack](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.8.20){: new_window} 内
提供了以下 Go 版本：

* 1.6.3
* 1.6.4
* 1.7.5
* 1.7.6
* 1.8.6
* 1.8.7
* 1.9.3
* 1.9.4
* 1.10

如果您应用程序所需的 Go 版本没有列在上述列表中，那么可以使用外部 [Go buildpack](https://github.com/cloudfoundry/go-buildpack.git){: new_window} 来部署应用程序。

# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}

* [GoLang](http://golang.org/){: new_window}
* [用于 Go 的 Cloud Foundry buildpack](https://github.com/cloudfoundry/go-buildpack){: new_window}
