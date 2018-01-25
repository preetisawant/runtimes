---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# ASP.NET Core
{: #dotnet_core}

O tempo de execução ASP.NET Core no {{site.data.keyword.Bluemix}} é desenvolvido com o buildpack ASP.NET Core. O ASP.NET Core
é uma estrutura de software livre modular para a construção de aplicativos da web .NET.
O .Net Core é um tempo de execução pequeno de plataforma cruzada que pode ser direcionado pelos aplicativos ASP.NET Core.
Eles combinam para permitir aplicativos da web modernos, baseados em nuvem.
{: shortdesc}

## Detecção
{: #detection}
O {{site.data.keyword.Bluemix}} buildpack do ASP.NET Core é usado se houver uma ou mais pastas contendo um arquivo
project.json e pelo menos um arquivo .cs em qualquer lugar no aplicativo ou se o aplicativo for enviado por push do diretório de
saída do comando *dotnet publish*.

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix_notm}} fornece um aplicativo iniciador do ASP.NET Core.  O aplicativo iniciador do ASP.NET Core é um app simples que fornece um modelo que pode ser usado. É possível experimentar o app iniciador, fazendo e enviando mudanças por push para o ambiente
{{site.data.keyword.Bluemix_notm}}.  Consulte [Usando os aplicativos iniciadores](/docs/cfapps/starter_app_usage.html) para obter ajuda sobre o uso
do aplicativo iniciador.

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [NuGet](https://docs.nuget.org/Consume/Overview){: new_window}
* [Visão geral do ASP.NET Core](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html){: new_window}
