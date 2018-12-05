---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# カスタム・ネイティブ・ライブラリーの使用
{: #use_customlib}

ライブラリーによっては、NuGet パッケージとネイティブ・ライブラリー・ファイル (`.so` ファイル) の両方の使用を必要とするものがあります。  

これらのライブラリーをビルドパックで使用するには、それらをアプリケーションのルート・フォルダー内の `ld_library_path` フォルダーに入れます。ビルドパックは、ステージング時にこのパスを `LD_LIBRARY_PATH` 環境変数に自動的に追加します。  

あるいは、アプリケーションの `manifest.yml` ファイルで、または `ibmcloud cf set-env` コマンドを使用することによって、`ld_library_path` 以外のフォルダー名を使用するように `LD_LIBRARY_PATH` 環境変数を指定できます。その場合、ビルドパックは、ビルドパックによって生成される `LD_LIBRARY_PATH` にそのカスタム・パスを追加します。
