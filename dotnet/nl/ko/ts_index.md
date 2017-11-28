---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 문제점 해결 FAQ
{: #troubleshooting_faq}

**질문**: 애플리케이션 배치에 실패하고 다음 메시지가 표시됩니다. `API/0App instance exited ... payload: {... "reason"=>"CRASHED", "exit_status"=>-1, ...}`.  이는 어떤 의미입니까? 

**답변**: 애플리케이션을 푸시할 때 이와 비슷한 메시지를 받는 경우 이는 애플리케이션이 메모리나 디스크 할당량 한계를 초과했기 때문일 가능성이 매우 높습니다. 애플리케이션의 할당량을 늘리면 해결됩니다. 

**질문**: 내 애플리케이션이 배치에 실패하며 다음 메시지가 나타납니다. `Failed to compress droplet: signal: broken pipe` 또는 `No space left on device`. 이 문제의 해결 방법은 무엇입니까?

**답변**: 많은 수의 NuGet 패키지 종속 항목이 포함된 소스 코드에서 푸시된 프로젝트로 인해 NuGet 패키지 캐시를 사용할 때 종종 이 오류가 발생합니다. 캐시를 사용 안함으로 설정하려면 `CACHE_NUGET_PACKAGES` 환경 변수를 `false`로 설정하십시오. 자세한 정보는 [NuGet 패키지를 사용 안함](diablingNuGet.md)으로 설정하는 방법에 대한 지시사항을 참조하십시오. 

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [ASP.NET Core 개요](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
