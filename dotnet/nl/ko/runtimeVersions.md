---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 런타임 버전
{: #runtime_vertsions}


{: shortdesc}

## 지원되는 버전
{: #supported_versions}
이 빌드팩은 다음 버전을 지원하며, 더 이상 사용되지 않음으로 표시된 버전은 향후 빌드팩 릴리스에서 제거됩니다.  [LTS 및 현재 릴리스에 대한 Microsoft의 지원 설명](https://www.microsoft.com/net/core/support)을 참조하십시오.

### project.json 도구(더 이상 사용되지 않음)

| .NET SDK 버전        | 기본값 |
|-------------------------|---------|
| 1.0.0-preview2-003156   |   아니오    |

### MSBuild SDK 도구

| .NET SDK 버전        | 기본값 |
|-------------------------|---------|
| 1.0.3                   |   아니오    |
| 1.0.4                   |   예   |
| 1.1.0-preview1-005051   |   아니오    |
| 2.0.0-preview1-005977   |   아니오    |
| 2.0.0-preview2-006497   |   아니오    |

### .NET Core 런타임 버전

| .NET Core 런타임 버전 | 릴리스 유형  | 기본값 |
|---------------------------|---------------|---------|
| 1.0.3(더 이상 사용되지 않음)        | LTS           |   아니오    |
| 1.0.4(더 이상 사용되지 않음)        | LTS           |   아니오    |
| 1.0.5                     | LTS           |   예   |
| 1.1.0(더 이상 사용되지 않음)        | 현재       |   아니오    |
| 1.1.1(더 이상 사용되지 않음)        | 현재       |   아니오    |
| 1.1.2                     | 현재       |   아니오    |
| 2.0.0-preview1-002111-00  | LTS(미리보기) |   아니오    |
| 2.0.0-preview2-25407-01   | LTS(미리보기) |   아니오    |

## .NET SDK 버전 지정

애플리케이션의 루트 디렉토리에 있는 선택적인 global.json으로 .NET SDK 버전을 제어하십시오. 예를 들어, 다음과 같습니다.
```
   {
      "sdk": {
        "version": "2.0.0-preview2-006497"
      }
   }
```
{: codeblock}

지정되지 않은 경우 최신 LTS(Long-term-support) GA 런타임의 MSBuild 도구가 사용됩니다.  project.json 도구를 사용하기 위해 위에 나열된 project.json 버전 중 하나를 지정할 수 있지만 향후에 이러한 버전이 제거된다는 점에 유의해야 합니다.
