---

copyright:
  years: 2019
lastupdated: "2019-02-01"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 월별 런타임 사용
{: #using_monthly_runtime}

Liberty 월별 런타임은 최신 버전, 새 기능 및 프로그래밍 모델에 대한 액세스를 제공합니다.

{{site.data.keyword.Bluemix_notm}}에서 Liberty 월별 런타임을 사용하려면 다음 작업을 수행해야 합니다.

`JBP_CONFIG_LIBERTY` 환경 변수를 `"version: +"`로, `IBM_LIBERTY_MONTHLY` 환경 변수를 `true`로 설정하십시오. 이러한 변수는 [Liberty 월별 런타임](/docs/runtimes/liberty/buildpackDefaults.html#liberty_versions)을 사용할 수 있도록 합니다. 예를 들어, 다음과 같습니다.
  * {{site.data.keyword.Bluemix_notm}} CLI 도구 사용:
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_MONTHLY true
    ```
    {: .codeblock}

  * 또는, `manifest.yml` 파일을 사용합니다.
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
          IBM_LIBERTY_MONTHLY: true
    ```

    ```
      env:
          JBP_CONFIG_LIBERTY: "[version: +, app_archive: {features: [javaee-8.0]}]"
          IBM_LIBERTY_MONTHLY: true
    ```
    {: .codeblock}

기존 애플리케이션에서 월별 런타임을 사용으로 설정하는 경우에는 환경 변수를 설정한 다음 애플리케이션을 삭제한 후 다시 푸시해야 할 수 있습니다.
