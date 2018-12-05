---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 사용자 정의 네이티브 라이브러리 사용
{: #use_customlib}

일부 라이브러리에서는 NuGet 패키지와 일부 네이티브 라이브러리 파일(`.so` 파일)을 둘 다 사용해야 합니다.    

빌드팩에서 이러한 라이브러리를 사용하려면, 애플리케이션의 루트 폴더 내의 `ld_library_path` 폴더에 라이브러리를 넣으십시오. 빌드팩은 스테이징 중에 이 경로를 `LD_LIBRARY_PATH` 환경 변수에 자동으로 추가합니다.    

또는 애플리케이션의 `manifest.yml` 파일에 `LD_LIBRARY_PATH` 환경 변수를 지정하거나 `ibmcloud cf set-env` 명령을 사용하여 `ld_library_path`가 아닌 다른 폴더 이름을 사용할 수 있습니다. 이 경우 빌드팩은 이 사용자 정의 경로를 빌드팩에서 생성된 `LD_LIBRARY_PATH`에 추가합니다.
