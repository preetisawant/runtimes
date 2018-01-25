---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

Os aplicativos Liberty for Java no {{site.data.keyword.Bluemix}} são desenvolvidos pelo buildpack liberty-for-java. O buildpack liberty-for-java fornece um ambiente de tempo de execução completo para executar os aplicativos Java EE 7 e OSGi na parte superior do perfil Liberty. 
Ele suporta estruturas populares como Spring e inclui o {{site.data.keyword.IBM_notm}} JRE. O WebSphere Liberty permite o desenvolvimento rápido de aplicativo, o que é bem adequado para a nuvem.
{: shortdesc}

## Detecção
{: #detection}
O buildpack do Liberty é usado quando os tipos de aplicativos a seguir são implementados:
* [Arquivos WAR](optionsForPushing.html#stand_alone_apps)
* [Arquivos EAR](optionsForPushing.html#stand_alone_apps)
* [Diretório do servidor Liberty](optionsForPushing.html#server_directory)
* [Servidor em pacote Liberty](optionsForPushing.html#packaged_server)
* Java principal
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## Aplicativo iniciador
{: #starter_application}
O {{site.data.keyword.Bluemix_notm}} fornece vários aplicativos iniciadores Liberty. Os aplicativos iniciadores Liberty são apps Liberty simples que fornecem um modelo que pode ser usado. 
É possível experimentar os aplicativos iniciadores e fazer e enviar mudanças por push para o ambiente {{site.data.keyword.Bluemix_notm}}. Veja [Usando os aplicativos iniciadores](/docs/cfapps/starter_app_usage.html) para obter ajuda sobre o uso dos aplicativos iniciadores.

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Visão geral do perfil Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [Gerenciando apps Liberty](/docs/manageapps/app_mng.html#Utilities)
* [Implementando aplicativos com o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [Introdução ao IBM Monitoring and Analytics for {{site.data.keyword.Bluemix_notm}} Service](/docs/services/monana/index.html#monana_oview)
