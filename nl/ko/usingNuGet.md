---

copyright:
  years: 2015, 2018
lastupdated: "2017-05-31"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# NuGet 패키지 소스 사용자 정의 정보
{: #customizing_nuget}
애플리케이션의 루트 디렉토리에 있는 NuGet.Config 파일을 사용하여 애플리케이션의 종속 항목이 다운로드되는 위치를 제어할 수 있습니다. 다음 예에서 `<packageSources>` 특성을 구성하면 애플리케이션의 키와 API URL을 정의하여 패키지를 검색합니다.
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}
