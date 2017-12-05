---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# カスタム・ライブラリーについて
{: #use_customlib}

{: #shortdesc}

## カスタム・ネイティブ・ライブラリーの使用
{: #using_custom_native_libraries}

一部のライブラリーでは、NuGet パッケージとネイティブ・ライブラリー・ファイル (.so ファイル) の両方を使用する必要がある場合があります。ビルドパックでこれらのライブラリーを使用するには、アプリケーションのルート・フォルダー内の *ld_library_path* という名前のフォルダーに当該ライブラリーを配置する必要があります。
ビルドパックでは、ステージング時に、このパスが `LD_LIBRARY_PATH` 環境変数に自動的に追加されます。あるいは、アプリケーションの `manifest.yml` ファイルで、または `cf set-env` コマンドを使用して、*ld_library_path* 以外のフォルダー名を使用するように `LD_LIBRARY_PATH` 環境変数を指定できます。その場合、ビルドパックでは、ビルドパックによって生成される `LD_LIBRARY_PATH` にそのカスタム・パスが追加されます。
