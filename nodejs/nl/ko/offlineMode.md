---

copyright:
  years: 2016, 2018
lastupdated: "2018-07-12"
subcollection: "Nodejs"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Node.js를 사용하여 오프라인으로 작업
{: #offline_mode}

Node.js 애플리케이션이 {{site.data.keyword.Bluemix}}에 푸시되는 경우, SDK for Node.js 빌드팩은 일반적으로 외부 리소스(예: NPM의 노드 모듈)에서 아티팩트를 다운로드합니다.  [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 및 [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local)에서와 같은 일부 상황에서는 {{site.data.keyword.Bluemix_notm}}에 외부적인 사이트에 대한 액세스를 사용자 정의할 수 있습니다.  
{: shortdesc}

Node.js 빌드팩은 다음의 외부 사이트에 액세스할 수 있습니다. [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 및 [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) {{site.data.keyword.Bluemix_notm}} 환경에서는 이러한 사이트를 *화이트리스트*에 추가해야 합니다.

* 다음은 사용 가능한 노드 엔진 버전을 확인하는 데 사용될 수 있습니다. http://nodejs.org/
* 다음은 빌드팩에 포함되지 않은 노드 엔진 버전을 검색하는 데 사용됩니다. https://s3pository.heroku.com
*  다음은 빌드팩에 포함되지 않은 npm의 버전을 검색하는 데 사용됩니다. https://www.npmjs.com/package/npm 및 https://semver.herokuapp.com
* https://iojs.org 사이트가 빌드팩에 포함되어 있지 않거나 다음에서 사용 가능하지 않은 이전 버전의 노드를 검색하는 데 사용됩니다. https://semver.herokuapp.com
* 다음은 express 등의 노드 모듈을 검색하는 데 사용됩니다. https://registry.npmjs.org

화이트리스트에 추가된 사이트 세트를 최소화하려면 SDK for Node.js 빌드팩에 포함된 노드 엔진 버전을 사용하도록 애플리케이션을 구성하십시오.  빌드팩에 포함된 노드 엔진 버전 세트는 [최신 업데이트](/docs/runtimes/nodejs/updates.html)를 참조하십시오.  이러한 노드 엔진 버전을 사용하도록 애플리케이션을 구성한 경우에는 https://registry.npmjs.org 사이트만 모듈 다운로드에 필요합니다.

새 버전의 SDK for Node.js 빌드팩이 설치되면 사용 가능한 엔진 버전 세트가 종종 보다 최신 버전으로 변경된다는 점을 유념하십시오.  빌드팩에 포함된 보다 최신의 노드 엔진 버전을 지정하기 위해 앱을 재구성해야 할 수 있습니다.


## 오프라인 애플리케이션
{: #offline_applications}

별도로 https://registry.npmjs.org에 액세스할 필요가 없도록, 애플리케이션이 요구하는 모든 노드 모듈을 애플리케이션 내에 포함시킬 수 있습니다.  이를 수행하려면 모든 필수 애플리케이션 모듈에 대해 `npm install`을 실행한 후에 푸시된 애플리케이션의 `node_modules` 디렉토리를 포함하십시오.

종속 항목에는 종속 항목이 포함될 수 있으며 반복해서 이에 다시 종속 항목이 포함될 수 있지만, `package.json`에는 최상위 레벨 종속 항목만 포함됩니다. 종속 항목 중 하나가 릴리스되는 새 버전 및 package.json의 범위를 사용하는 경우, `node_modules` 디렉토리의 모듈은 더 이상 사용할 수 없습니다. 이를 막기 위해 *Shrinkwrap*이 모든 종속 항목 버전을 잠그는 데 도움이 됩니다.  shrinkwrap을 사용하려면 비어 있거나 정리된 `node_modules` 디렉토리에서 시작하십시오. 그런 다음 프로젝트의 루트 디렉토리에서 다음 명령을 실행하십시오.

```
npm install
```
{: codeblock}

```
npm dedupe
```
{: codeblock}

```
npm shrinkwrap
```
{: codeblock}

그러면 루트 디렉토리에서 `package.json`이 변경되고 `npm-shrinkwrap.json`이 추가될 수 있습니다.
`package.json` 파일의 종속 항목을 변경할 때마다 `npm dedupe` 및 `shrinkwrap` 명령을 재실행하십시오.

## 프록시 작업
{: #working_with_proxy}

[{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) 및 [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) 등의 일부 환경에서는 프록시의 구성이 가능합니다. 자세한 내용은
[프록시 작업](/docs/runtimes-common/workingWithProxy.html)을 참조하십시오.
