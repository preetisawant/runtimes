---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 런타임 버전
{: #runtime_versions}


{: shortdesc}

## 지원되는 버전
{: #supported_versions}

이 빌드팩은 다음 버전을 지원하며, 더 이상 사용되지 않음으로 표시된 버전은 향후 빌드팩 릴리스에서 제거됩니다.  [LTS 및 현재 릴리스에 대한 Microsoft의 지원 설명](https://www.microsoft.com/net/core/support)을 참조하십시오.

### project.json 도구(더 이상 사용되지 않음)

|.NET SDK 버전        |기본값 |
|-------------------------|---------|
|1.0.0-preview2-003156   |아니오    |

### MSBuild SDK 도구

|.NET SDK 버전        |기본값          |
|-------------------------|------------------|
|1.0.4                   |아니오             |
| 1.1.0                   |예(F#만 해당)  |
| 2.0.0                   |예            |

### .NET Core 런타임 버전

|.NET Core 런타임 버전 |릴리스 유형      |
|---------------------------|-------------------|
|1.0.4(더 이상 사용되지 않음)        |LTS               |
|1.0.5                     |LTS               |
|1.1.1(더 이상 사용되지 않음)        |LTS               |
|1.1.2                     |LTS               |
|2.0.0-preview2-25407-01   |현재(미리보기) |
| 2.0.0                     |현재           |

## .NET SDK 버전 지정

애플리케이션의 루트 디렉토리에 있는 선택적인 `global.json` 파일로 .NET SDK 버전을 제어하십시오. 예를 들어, 다음과 같습니다.
```
   {
      "sdk": {
        "version": "2.0.0"
      }
   }
```
{: codeblock}

이를 지정하지 않으면 최신 MSBuild 도구가 사용됩니다.  project.json 도구를 사용하기 위해 나열된 project.json 버전 중 하나를 지정할 수 있지만 향후에 이러한 버전이 제거된다는 점에 유의해야 합니다.  지정된 버전이 빌드팩에 없는 경우 기본 버전이 사용되며 스테이징 로그에 경고가 표시됩니다.
