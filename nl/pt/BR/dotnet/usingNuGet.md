---

copyright:
  years: 2015, 2018
lastupdated: "2017-05-31"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Customize as fontes do pacote NuGet
{: #customizing_nuget}

É possível usar o arquivo `NuGet.Config` no diretório-raiz do aplicativo para controlar onde o aplicativo faz download das dependências. No exemplo a seguir, a configuração da propriedade `<packageSources>` define qualquer chave e URL de API para que o aplicativo recupere pacotes.
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}
