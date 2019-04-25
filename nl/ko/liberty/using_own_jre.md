---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-27"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 고유 JRE 사용
{: #using_own_jre}

고유 JRE를 사용하여 {{site.data.keyword.Bluemix}}에서 Liberty 애플리케이션을 실행할 수 있습니다. liberty-for-java 빌드팩은 [WebSphere Liberty에서 지원하는 런타임](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_restrict.html#rwlp_restrict__rest13)에 대한 지원을 제공하지만, 지원되지 않는 버전의 전체 기능을 보장하지는 않습니다. 애플리케이션에서 JRE를 사용할 수 있게 하려면 다음을 완료해야 합니다.
* 빌드팩이 다운로드할 수 있는 위치에서 JRE를 호스팅하십시오.
* JRE의 위치를 제공하는 `index.yml` 파일을 호스팅하십시오.
* JRE를 사용하도록 애플리케이션을 구성하십시오.

## JRE 및 `index.yml` 호스팅
{: #hosting_jre}

liberty-for-java 빌드팩이 다운로드할 수 있는 웹 서버에서 JRE 파일을 호스팅해야 합니다. 사용 가능한 서버 시설을 사용하여 {{site.data.keyword.Bluemix_notm}}에서 파일을 호스팅하거나 공용으로 사용 가능한 위치에서 호스팅할 수 있습니다. 서버는 JRE 파일에 대한 세부사항을 지정하는 `index.yml` 파일로 구성되어야 합니다.

다음 단계를 완료하여 JRE 및 `index.yml` 파일을 호스팅하십시오.
  1. JRE를 얻으십시오. 이 JRE는 UNIX 64비트 OS에서 사용할 버전이어야 하며 `tar.gz` 파일이어야 합니다.
  2. liberty-for-java 빌드팩이 다운로드할 수 있는 위치에서 JRE 파일을 호스팅하십시오.
  3. 호스팅 위치에서 `index.yml` 파일을 제공하십시오. `index.yml` 파일에는 JRE의 버전 ID를 포함하는 항목 다음에 콜론과 전체 JRE 파일 위치 URL이 포함되어야 합니다.
    * `index.yml` 파일에 JRE 버전을 정의하십시오.

    ```
    ---
    jre_version: https://hostingLocation/jreName.tar.gz
    ```
    {: codeblock}

    * JRE 버전 ID와 전체 JRE 파일 위치를 포함하십시오.  예를 들어, 다음과 같습니다.

    ```
    ---
    1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```
    {: codeblock}

## 앱 구성
{: #configure_app}

대체 JRE를 사용하도록 빌드팩을 구성하려면 Liberty 애플리케이션에서 두 개의 환경 변수를 설정해야 합니다. **JBP_CONFIG_OPENJDK**를 설정하여 `index.yml` 파일의 위치를 식별하고 **JVM** 환경 변수를 *openjdk*로 설정하십시오. 버전-값 문자열의 형식에 대한 자세한 정보는 [버전 구문과 순서 지정 및 와일드카드 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/util-repositories.md){: new_window}에서 Cloud Foundry 문서를 참조하십시오.

**JBP_CONFIG_OPENJDK** 변수의 값은 `index.yml` 파일 위치 및 index.yml 파일에서 선택할 JRE 버전입니다.

```
'{repository_root: "https://locationToIndexYml", version: version-value}'
```
{: codeblock}

`ibmcloud cf se myAPP` 명령을 실행하여 **JBP_CONFIG_OPENJDK** 변수를 설정하십시오. 예를 들어 다음과 같습니다.
```
ibmcloud cf se myApp JBP_CONFIG_OPENJDK '{repository_root: "https://myHostingApp.ng.bluemix.net", version: 1.8.+}'
```
{: codeblock}

*repository_root* URL에는 URL의 `index.yml`이 포함되지 않습니다. *repository_root* URL은 파일 자체가 아니라 `index.yml` 파일을 포함하는 디렉토리 레벨을 가리킵니다.

JVM 환경 변수를 설정하려면 다음 명령을 실행하십시오.
```
ibmcloud cf se myApp JVM 'openjdk'
```
{: codeblock}

**참고**: 변경을 적용하려면 환경 변수를 설정한 후에 애플리케이션을 다시 스테이징하십시오.

## 확인
{: #confirmation}

Liberty에서 예상 JRE를 사용하는지 확인하려면 스테이징 로그를 확인하십시오. 서버에서 `index.yml` 파일에 표시된 위치에서 빌드팩을 다운로드했음을 표시하는 메시지를 찾으십시오. Liberty에서 예상 JRE를 성공적으로 사용할 때 로그 출력의 예는 다음 스니펫을 참조하십시오.
```
 -----> Downloading OpenJdk 1.8.0_91 from
  https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}
