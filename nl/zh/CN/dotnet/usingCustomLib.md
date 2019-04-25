---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 使用定制本机库
{: #use_customlib}

某些库可能需要使用 NuGet 数据包和一些本机库文件（`.so` 文件）。  

要将这些库与 buildpack 一起使用，请将这些库放入应用程序根文件夹内的 `ld_library_path` 文件夹中。buildpack 在编译打包期间自动将此路径添加到 `LD_LIBRARY_PATH` 环境变量。  

或者，您可以在应用程序的 `manifest.yml` 文件中指定 `LD_LIBRARY_PATH` 环境变量，也可以使用 `ibmcloud cf set-env` 命令来设置不同于 `ld_library_path` 的文件夹名称。在这种情况下，buildpack 会将此定制路径附加到 buildpack 生成的 `LD_LIBRARY_PATH`。
