---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 关于定制库
{: #use_customlib}

{: #shortdesc}

## 使用定制本机库
{: #using_custom_native_libraries}

某些库可能需要使用 NuGet 数据包和一些本机库文件（.so 文件）。为了将这些库与 buildpack 一起使用，应该将这些库放入应用程序根文件夹中名为 *ld_library_path* 的文件夹中。
buildpack 将在编译打包期间自动将此路径添加到 `LD_LIBRARY_PATH` 环境变量。或者，您可以在应用程序的 `manifest.yml` 文件中指定 `LD_LIBRARY_PATH` 环境变量，也可以通过 `cf set-env` 命令使用不同于 *ld_library_path* 的文件夹名称。在这种情况下，buildpack 会将此定制路径附加到 buildpack 生成的 `LD_LIBRARY_PATH`。
