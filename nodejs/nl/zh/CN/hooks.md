---

copyright:
  years: 2018
lastupdated: "2018-11-09"
subcollection: "Nodejs"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# 使用挂钩集成第三方服务
{: #hooks}

可以使用挂钩轻松在 SDK for Node.js buildpack 中集成第三方服务。请注意，IBM 对您集成的任何第三方服务都不提供支持。有关支持的更多信息，请参阅[第三方服务](/docs/runtimes-common/buildpackSupport.html#third-party)。

SDK for Node.js buildpack 包含 Dynatrace 挂钩。Dynatrace 启用 Node.js 应用程序的应用程序监视。了解 [Dynatrace 文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")]( https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/application-only/deploy-oneagent-on-cloud-foundry-for-application-only-monitoring/){: new_window} 内有关在 buildpack 中使用 Dynatrace 挂钩的更多信息。


遵循第三方文档中的指示信息时，请记得使用 `ibmcloud cf` 命令而非 `cf` 来运行 {{site.data.keyword.Bluemix_notm}} buildpack 的命令。
{: tip}
