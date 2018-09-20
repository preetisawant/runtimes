---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}

O tempo de execução do Tomcat no {{site.data.keyword.Bluemix}} foi desenvolvido com o java_buildpack.
{: shortdesc}

Para usar o runtime do Tomcat no {{site.data.keyword.Bluemix_notm}}, deve-se especificar o java_buildpack
com a opção `-b`. Por exemplo:

```
ibmcloud cf push <myApp> -p <pathToMyApp> -b java_buildpack
```

Para obter mais informações sobre o tempo de execução do Tomcat, veja o
[leia-me do java-buildpack](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md).

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix_notm}} fornece um aplicativo iniciador do Tomcat.  O aplicativo iniciador do Tomcat é um app Tomcat simples que fornece um modelo que pode ser usado. É possível experimentar o app iniciador, fazendo e enviando mudanças por push para o ambiente
{{site.data.keyword.Bluemix_notm}}. Consulte [Usando os aplicativos iniciadores](../common/starter_app_usage.html) para obter ajuda sobre o uso
do aplicativo iniciador.

## Versões de tempo de execução
{: #runtime_versions}

É possível mudar a versão do Tomcat a ser usada por seu app com a variável de ambiente JBP_CONFIG_TOMCAT.
É possível mudar a versão do Java a ser usada por seu app com a variável de ambiente JBP_CONFIG_OPEN_JDK_JRE.
Ambos podem ser especificados no arquivo manifest do aplicativo.  Por exemplo:
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.5.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.8.0_+ }}'
```
{: codeblock}
A versão do java_buildpack atual é a v4.9, que contém a versão 8.5.28 do Tomcat padrão e a versão 1.8.0_162 do Java padrão.
Para obter mais informações, consulte [Liberações java-buildpack](https://github.com/cloudfoundry/java-buildpack/releases/tag/v4.9).

## Redirecionamento de HTTPS
{: #https_redirect}

O tempo de execução do Tomcat pode ser configurado para confiar em proxies internos do
{{site.data.keyword.Bluemix_notm}} e permitir o redirecionamento de tráfego HTTP para HTTPS (SSL).
Para fazer isso, modifique o arquivo `server.xml`, configurando o elemento Valve `RemoteIpValve` com as opções `internalProxies` e `protocolHeader`.

Por padrão, o [server.xml](https://github.com/cloudfoundry/java-buildpack/blob/master/resources/tomcat/conf/server.xml)
do runtime do Tomcat incluído no buildpack configura apenas o `protocolHeader` do elemento Valve
`RemoteIpValve`.  Para redirecionar o tráfego HTTP para HTTPS no {{site.data.keyword.Bluemix_notm}},
configure o elemento `RemoteIpValve` no `server.xml` customizado, conforme mostrado no exemplo a seguir:

```
 <Valve className='org.apache.catalina.valves.RemoteIpValve' protocolHeader='x-forwarded-proto' internalProxies='.*' />
```
{: codeblock}

Mais opções de configuração para o RemoteIpValve podem ser localizadas na
[documentação do Tomcat ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://tomcat.apache.org/tomcat-8.5-doc/api/org/apache/catalina/valves/RemoteIpValve.html).
