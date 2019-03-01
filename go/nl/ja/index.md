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

{{site.data.keyword.Bluemix}} の Go ランタイムには go_buildpack が採用されています。
go_buildpack は、Go アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

go_buildpack は、アプリケーションに *.go という名前のファイルが含まれている場合に使用されます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} には、Go スターター・アプリケーションが用意されています。  Go スターター・アプリケーションは、アプリケーションで使用可能なテンプレートを提供する、シンプルな Go アプリケーションです。 スターター・アプリケーションを試し、{{site.data.keyword.Bluemix_notm}} 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](docs/runtimes-common/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

アプリケーションのルートにある Godeps/Godeps.json ファイルで GoVersion プロパティーを設定することにより、アプリケーションで使用する Go のバージョンを指定できます。 例えば、次のように指定します。

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.10",
	"Deps": []
}
```
{: codeblock}
詳しくは、[『godep』](https://github.com/tools/godep){: new_window}を参照してください。

バージョンを指定しない場合は、デフォルトでバージョン 1.8.7 が選択されます。

### 使用可能なバージョン:
{: #available_versions}

現在 {{site.data.keyword.Bluemix_notm}} にインストールされている [Go ビルドパック](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.8.20){: new_window}では、以下のバージョンの Go が使用できます。

* 1.6.3
* 1.6.4
* 1.7.5
* 1.7.6
* 1.8.6
* 1.8.7
* 1.9.3
* 1.9.4
* 1.10

アプリケーションが、リストされていないバージョンの Go を必要とする場合は、外部の [Go ビルドパック](https://github.com/cloudfoundry/go-buildpack.git){: new_window}を使用してアプリケーションをデプロイできます。
