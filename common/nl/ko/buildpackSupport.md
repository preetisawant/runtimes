---

copyright:
  years: 2016, 2018
lastupdated: "2018-01-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 빌드팩 지원 구문
{: #buildpack_support_statement}


## 기본 제공 IBM 빌드팩
{: #built-in_ibm_buildpacks}

[Liberty for Java](/docs/runtimes/liberty/index.html), [SDK for Node.js](/docs/runtimes/nodejs/index.html) 및 [ASP.NET Core](/docs/runtimes/dotnet/index.html)의 경우, IBM은 두 개의 버전(n & n - 1)을 지원합니다(예: IBM Liberty 빌드팩 v3.12 & IBM Liberty 빌드팩 v3.11). 상황에 맞게, 각각의 빌드팩은 대응되는 런타임의 하나 이상의 주 버전을 제공하고 지원합니다. 빌드팩은 일반적으로 사용 가능한 런타임의 최신 부 버전으로 매월 한 번씩 새로 고쳐집니다. 

[IBM {{site.data.keyword.Bluemix_notm}} Runtime for Swift](/docs/runtimes/swift/index.html)의 경우, IBM은 [Swift.org](http://swift.org)에서 사용 가능한 최신 Swift 버전과 일치하는 빌드팩에 대한 지원을 제공합니다. 빌드팩에 대한 업데이트는 사용 가능한 최신 Swift 릴리스 버전과 일치합니다. 

{{site.data.keyword.Bluemix_notm}}에서 현재 지원되는 기본 제공 IBM 빌드팩의 임의의 버전에 대해 문제점/이슈를 보고할 수 있지만, 이는 최신 버전에 대해 확인되어야 합니다. 결함이 발견되는 경우, IBM은 이후 레벨의 런타임 및 대응되는 빌드팩에서 수정사항을 제공합니다. IBM은 이전의 주 버전과 부 버전(N-1, n-1)에 대해서는 수정사항을 제공하지 않습니다. IBM 빌드팩을 사용(예: Liberty 빌드팩의 Open JDK를 사용) 중인 경우에도 IBM은 커뮤니티 런타임에 대한 지원을 제공하지 않습니다. 이러한 커뮤니티 런타임은 아래의 "기본 제공 커뮤니티 빌드팩"과 동일한 지원 정책을 따릅니다. 

## 기본 제공 커뮤니티 빌드팩
{: #built-in_community_buildpacks}

Cloud Foundry 커뮤니티에서는 다음 기본 제공 커뮤니티 빌드팩을 제공합니다. 

* [Java](/docs/runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](/docs/runtimes/php/index.html)
* [Ruby](/docs/runtimes/ruby/index.html)
* [Python](/docs/runtimes/python/index.html)
* [Go](/docs/runtimes/go/index.html)

{{site.data.keyword.Bluemix_notm}}를 새 버전의 Cloud Foundry로 업그레이드하면 이러한 빌드팩에 대한 업데이트가 이루어집니다. {{site.data.keyword.Bluemix_notm}}에서 이러한 런타임의 문제점/이슈를 IBM에 보고할 수 있으며, IBM은 {{site.data.keyword.Bluemix_notm}}가 문제점의 원인인지 여부를 판별하는 데 도움을 줍니다. {{site.data.keyword.Bluemix_notm}} 관련 문제인 경우 IBM은 수정사항을 제공하지만, 빌드팩 또는 런타임 자체의 결함인 경우 IBM은 해당 커뮤니티에 이를 보고할 수 있도록 도움을 줍니다. IBM은 이러한 빌드팩 및 런타임에 대한 수정사항은 제공하지 않습니다. 

## 외부 빌드팩
{: #external_buildpacks}


외부 빌드팩의 경우에는 IBM에서 지원을 제공하지 않습니다. 지원을 받으려면 Cloud Foundry 커뮤니티에 문의해야 합니다. 
