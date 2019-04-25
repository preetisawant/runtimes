---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
subcollection: "Dotnet"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Use bibliotecas nativas customizadas
{: #use_customlib}

Algumas bibliotecas podem requerer o uso de um pacote NuGet e de alguns arquivos de biblioteca nativa (arquivos `.so`).  

Para usar essas bibliotecas com o buildpack, coloque-as em uma pasta `ld_library_path` dentro da pasta raiz do aplicativo. O buildpack inclui automaticamente esse caminho na variável de ambiente `LD_LIBRARY_PATH` durante a preparação.  

Como alternativa, é possível especificar a variável de ambiente `LD_LIBRARY_PATH` no arquivo `manifest.yml` do aplicativo ou usando o comando `ibmcloud cf set-env` para usar um nome de pasta diferente de `ld_library_path`.  Neste caso, o buildpack anexa esse caminho customizado ao `LD_LIBRARY_PATH` gerado pelo buildpack.
