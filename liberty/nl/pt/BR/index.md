---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-04"
subcollection: "liberty"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

Os aplicativos Liberty for Java no {{site.data.keyword.Bluemix}} são desenvolvidos pelo buildpack liberty-for-java. O
buildpack liberty-for-java fornece um ambiente de tempo de execução completo para executar aplicativos Java EE 7 e OSGi na parte superior do WebSphere Liberty. Ele suporta estruturas populares como Spring e inclui o {{site.data.keyword.IBM_notm}} JRE. O Liberty permite o desenvolvimento rápido do aplicativo que é bem adequado para a nuvem.
{: shortdesc}

## Detecção
{: #detection}
O buildpack do Liberty é usado quando os tipos de aplicativos a seguir são implementados:
* [Arquivos WAR](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)
* [Arquivos
EAR](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)
* [Diretório do servidor Liberty](/docs/runtimes/liberty/optionsForPushing.html#server_directory)
* [Servidor em pacote Liberty](/docs/runtimes/liberty/optionsForPushing.html#packaged_server)
* Java principal
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## Aplicativo iniciador
{: #starter_application}
O {{site.data.keyword.Bluemix_notm}} fornece vários aplicativos iniciadores Liberty.  Os aplicativos iniciadores Liberty são apps Liberty simples que fornecem um modelo que pode ser usado. É possível experimentar os aplicativos iniciadores e fazer e enviar mudanças por push para o ambiente {{site.data.keyword.Bluemix_notm}}.  Veja [Usando os aplicativos iniciadores](/docs/runtimes-common/starter_app_usage.html) para obter ajuda sobre o uso dos aplicativos iniciadores.
