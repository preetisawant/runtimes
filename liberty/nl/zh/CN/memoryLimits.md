---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 内存限制和 Liberty buildpack
{: #memory_limits}

使用 Liberty buildpack 部署应用程序时，必须指定内存限制。

## 内存限制和 Liberty buildpack
{: #memory_limits_and_liberty}


使用 Liberty buildpack 部署应用程序时，会提示您输入“内存限制”。Liberty for Java buildpack 设置缺省堆内存大小比率以防止进程超过内存限制。还可以通过定义 `JVM_ARGS` 或 `JBP_CONFIG_IBMJDK` 环境变量来指定堆内存大小或比率。请参阅[堆内存选项](#heap_memory_options)以了解更多信息。

要确定指定多大的“内存限制”，请务必了解您并不是在指定 Java 应用程序堆的大小。您要指定 Diego 容器或 DEA 要使用的可用内存量。此内存量包括以下组件使用的内存：

* warden 容器要使用的内存量。
* 用于将内核扩展和系统库映射到进程的内存量。
* 用于 jvm 可执行文件、jvm 工作堆、jit 空间和压缩引用的内存量。
* 用于类（应用程序服务器和应用程序）、线程堆栈并定向到缓冲区的内存量。
* Java 应用程序堆要使用的内存量。

有关 JVM 内存使用量的更多信息，请查看 developerWorks 文章：[Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/)

部署应用程序时，将监视整个进程的内存使用量。如果内存使用量超出部署该应用程序指定的内存限制，那么内核会停止进程。此操作发生时不会有警告，可能会以几种方式体现。

 如果应用程序部署期间超出“内存限制”，您会收到发生故障的消息，还可能会看到以下情况。

  * 您可能会看到应用程序不太稳定。
  * 还可能会看到应用程序多次尝试启动，但始终不成功。
  * 您可能会收到一条消息，指示应用程序部署失败。

如果应用程序正在运行时超出“内存限制”，那么进程会停止，Cloud Foundry 会尝试重新启动应用程序。应用程序可能会重新启动，但在一段时间内不可用。

## 堆内存选项
{: #heap_memory_options}

可以通过各种方式定制分配给应用程序的最大堆内存量，包括使用 `JVM_ARGS` 环境变量，更改 `jvm.options` 文件，或设置控制 `heap_size_ratio` 的 `JBP_CONFIG_IBMJDK` 环境变量。如果未指定任何设置，buildpack 会使用缺省设置。

### 堆内存缺省值
{: .#heap_memory_defaults}
为了防止因超过内存限制而发生错误，Liberty for Java buildpack 根据您在部署应用程序时指定的内存限制来设置缺省堆大小比率。

* 内存限制小于 512M 的应用程序的堆大小比率是 50%
* 内存限制大于等于 512M 的应用程序堆大小比率是 75%

在使用环境变量指定堆内存时，将覆盖缺省堆大小比率。

### 指定堆内存
{: #specifying_heap_memory}

设置堆内存大小的方式是使用环境变量或更改 `jvm.options` 文件。在使用 `JVM_ARGS` 或 `JBP_CONFIG_IBMJDK` 环境变量时，将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 会让所有更改生效。通过更改 `jvm.options` 文件，也可以对堆大小配置的影响进行本地测试。

* 使用 `JVM_ARGS` 环境变量和 -Xmx 自变量。例如，要将最大堆大小设置为 512M，请使用以下命令，然后重新编译打包应用程序。

```
    $ cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* 使用 JBP_CONFIG_IBMJDK 环境变量来指定堆大小比率。heap_size_ratio 是浮点值，指定可以分配给堆多大的内存限制。例如，要将一半可用内存分配给堆（50% 或 0.50），请发出以下命令，然后重新编译打包应用程序。

```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}

* 如果应用程序是[服务器目录](optionsForPushing.html#server_directory)或[打包服务器](optionsForPushing.html#packaged_server)，请在 jvm.options 文件中指定 -Xmx 自变量。有关使用 `jvm.options` 文件及 Liberty 运行时的更多信息，请参阅[设置类属 JVM](http://www-01.ibm.com/support/docview.wss?uid=swg21596474)。  
