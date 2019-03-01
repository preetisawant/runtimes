---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 런타임 버전
{: #runtime_versions}

## 지원되는 버전
{: #supported_versions}

이 빌드팩은 다음 버전을 지원하며, 더 이상 사용되지 않음으로 표시된 버전은 향후 빌드팩 릴리스에서 제거됩니다.  [LTS 및 현재 릴리스에 대한 Microsoft의 지원 설명](https://www.microsoft.com/net/core/support)을 참조하십시오.


### .NET SDK 버전

|.NET SDK 버전        |기본값          |
|-------------------------|------------------|
| 2.1.403                 |예            |
| 2.1.302                 |아니오             |
| 2.0.3                   |아니오             |
| 1.1.11                  |아니오             |
| 1.1.10                  |아니오             |
|1.0.4                   |아니오             |


### .NET Core 런타임 버전

|.NET Core 런타임 버전 |릴리스 유형      |
|---------------------------|-------------------|
| 2.1.5                     |현재           |  
| 2.1.4                     |LTS               |
| 2.1.2                     |LTS               |
| 2.0.9                     |LTS               |
| 2.0.7                     |LTS               |
| 1.1.10                    |LTS               |
| 1.1.9                     |LTS               |
| 1.0.12                    |LTS               |
| 1.0.11                    |LTS               |


### .NET aspnetcore 버전

| .NET aspnetcore 버전 |릴리스 유형      |
|---------------------------|-------------------|
| 2.1.5                     |현재           |  
| 2.1.4                     |LTS               |
| 2.1.2                     |LTS               |



## .NET SDK 버전 지정

애플리케이션의 루트 디렉토리에 있는 선택적인 `global.json` 파일로 .NET SDK 버전을 제어하십시오. 예를 들어, 다음과 같습니다.
```
   {
      "sdk": {
        "version": "2.1.301"
      }
   }
```
{: codeblock}

이를 지정하지 않으면 최신 MSBuild 도구가 사용됩니다.  project.json 도구를 사용하기 위해 나열된 project.json 버전 중 하나를 지정할 수 있지만 향후에 이러한 버전이 제거된다는 점에 유의해야 합니다.  지정된 버전이 빌드팩에 없는 경우 기본 버전이 사용되며 스테이징 로그에 경고가 표시됩니다.
