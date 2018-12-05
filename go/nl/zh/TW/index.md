---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}

{{site.data.keyword.Bluemix}} 上的 Go 運行環境是採用 go_buildpack 技術。go_buildpack 為 Go 應用程式提供完整的運行環境。
{: shortdesc}

go_buildpack 用於您的應用程式包含名為 *.go 的檔案的情況。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} 提供 Go 入門範本應用程式。Go 入門範本應用程式是簡單的 Go 應用程式，提供可以讓您用於應用程式的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 {{site.data.keyword.Bluemix_notm}} 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](../common/starter_app_usage.html)。

## 運行環境版本
{: #runtime_versions}

您可以在應用程式根目錄的 Godeps/Godeps.json 檔案中設定 GoVersion 內容，以指定應用程式要使用的 Go 版本。例如：

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.10",
	"Deps": []
}
```
{: codeblock}
如需相關資訊，請參閱 [godep](https://github.com/tools/godep){: new_window}。



如果未指定版本，依預設會選擇 1.8.7 版。

### 可用的版本：
{: #available_versions}

目前安裝在 {{site.data.keyword.Bluemix_notm}} 中的 [Go 建置套件](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.8.20){: new_window}提供下列 Go 版本：

* 1.6.3
* 1.6.4
* 1.7.5
* 1.7.6
* 1.8.6
* 1.8.7
* 1.9.3
* 1.9.4
* 1.10

如果您的應用程式需要未列出的 Go 版本，則可以使用外部 [Go 建置套件](https://github.com/cloudfoundry/go-buildpack.git){: new_window}來部署該應用程式。
