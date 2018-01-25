---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 메모리 한계 및 Liberty 빌드팩
{: #memory_limits}

Liberty 빌드팩을 사용하여 애플리케이션을 배치할 때 메모리 한계를 지정해야 합니다.

## 메모리 한계 및 Liberty 빌드팩
{: #memory_limits_and_liberty}


Liberty 빌드팩을 사용하여 애플리케이션을 배치하면 "메모리 한계"를 묻는 프롬프트가 표시됩니다. Liberty for Java 빌드팩은 프로세스에서 메모리 한계가 초과하지 않도록 기본 힙 메모리 크기 비율을 설정합니다. 또한 `JVM_ARGS` 또는 `JBP_CONFIG_IBMJDK` 환경 변수를 정의하여 힙 메모리 크기 또는 비율을 정의할 수 있습니다. 자세한 내용은 [힙 메모리 옵션](#heap_memory_options)을 참조하십시오.

지정할 메모리 한계를 결정하기 위해서는, Java 애플리케이션 힙의 크기를 지정하는 것이 아니라는 것을 이해해야 합니다. 사용할 Diego 컨테이너 또는 DEA에 사용할 수 있는 메모리의 크기를 지정하는 것입니다. 이 크기에는 다음 컴포넌트에 사용되는 메모리가 포함됩니다.

* warden 컨테이너에 의해 사용됨
* 커널 확장기능과 시스템 라이브러리를 프로세스에 맵핑하는 데 사용됨
* jvm 실행 파일, jvm 작업 힙, jit 영역 및 압축된 참조에 사용됨
* 클래스(애플리케이션 서버 및 애플리케이션), 스레드 스택 및 직접 io 버퍼에 사용됨
* Java 애플리케이션 힙에 의해 사용됨

JVM 메모리 사용에 대한 자세한 정보는 developerWorks 문서 [Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/)에 있습니다.

애플리케이션을 배치할 때 전체 프로세스의 메모리 사용량이 모니터링됩니다. 메모리 사용량이 애플리케이션 배치 시 사용자가 지정한 메모리 한계를 초과하는 경우, 커널에서 프로세스가 중지됩니다. 이 조치는 경고 없이 발생하므로 여러 방법으로 알 수 있습니다.

 애플리케이션을 배치하는 동안 메모리 한계를 초과하면 오류가 발생했다는 메시지가 표시될 수 있습니다. 메시지는 다음과 같습니다.

  * 애플리케이션이 불안정하게 작동하는 것을 느낄 수 있습니다.
  * 애플리케이션에서 여러 차례 시작하려고 시도했지만 항상 실패하는 경우도 있습니다.
  * 애플리케이션 배치에 실패했다는 메시지가 표시되기도 합니다.

애플리케이션이 제공되고 있는 동안 메모리 한계를 초과하면 프로세스가 중지되고 Cloud Foundry에서 애플리케이션을 다시 시작하려고 시도합니다. 애플리케이션이 다시 시작될 수 있지만 일정 시간 동안 사용 불가능합니다.

## 힙 메모리 옵션
{: #heap_memory_options}

`JVM_ARGS` 환경 변수를 사용하거나 `jvm.options` 파일을 변경하거나 `heap_size_ratio`를 제어하는 `JBP_CONFIG_IBMJDK` 환경 변수를 설정하는 것과 같은 다양한 방법으로 애플리케이션에 할당된 최대 힙 메모리 양을 사용자 정의할 수 있습니다. 설정을 지정하지 않으면 빌드팩은 기본 설정을 사용합니다.

### 힙 메모리 기본값
{: .#heap_memory_defaults}
메모리 한계를 초과하는 오류가 발생하지 않도록 애플리케이션을 배치할 때 지정하는 메모리 한계에 따라 기본 힙 크기 비율을 설정합니다.

* 애플리케이션의 메모리 한계가 512M 미만이면 힙 크기 비율은 50%입니다.
* 애플리케이션의 메모리 한계가 512M 이상이면 힙 크기 비율은 75%입니다.

환경 변수를 사용하여 힙 메모리를 지정하는 경우 기본 힙 크기 비율을 대체합니다.

### 힙 메모리 지정
{: #specifying_heap_memory}

환경 변수를 사용하거나 `jvm.options` 파일을 변경하여 힙 메모리 크기를 설정할 수 있습니다. `JVM_ARGS` 또는 `JBP_CONFIG_IBMJDK` 환경 변수를 사용하는 경우 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 푸시할 때 변경사항이 적용됩니다. `jvm.options` 파일을 변경하여 힙 크기 구성에 미치는 영향도 로컬에서 테스트할 수 있습니다.

* `JVM_ARGS` 환경 변수 및 -Xmx 인수를 사용하십시오. 예를 들어, 최대 힙 크기를 512M으로 설정하려면 다음 명령을 사용한 다음 앱을 다시 스테이징하십시오.

```
    $ cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* JBP_CONFIG_IBMJDK 환경 변수를 사용하여 힙 크기 비율을 지정하십시오.  heap_size_ratio는 힙에 할당할 메모리 한계의 양을 지정하는 부동 소수점 값입니다.  예를 들어, 힙에 사용 가능한 메모리의 반(50% 또는 0.50)을 할당하려면 다음 명령을 실행하고 앱을 다시 스테이징하십시오.

```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}

* 애플리케이션이 [서버 디렉토리](optionsForPushing.html#server_directory) 또는 [패키지된 서버](optionsForPushing.html#packaged_server)인 경우 jvm.options 파일에서 -Xmx 인수를 지정하십시오. Liberty 런타임과 함께 `jvm.options` 파일 사용에 대한 자세한 정보는 [Setting generic JVM](http://www-01.ibm.com/support/docview.wss?uid=swg21596474)을 참조하십시오.  
