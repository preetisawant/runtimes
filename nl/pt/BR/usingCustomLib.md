---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Sobre bibliotecas customizadas
{: #use_customlib}

{: #shortdesc}

## Usando bibliotecas nativas customizadas
{: #using_custom_native_libraries}

Algumas bibliotecas podem requerer o uso de um pacote NuGet e alguns arquivos de biblioteca nativa (arquivos .so).  Para usar essas bibliotecas com o buildpack, é necessário colocá-las em uma pasta chamada *ld_library_path* na pasta raiz do seu aplicativo.
O buildpack incluirá automaticamente esse caminho na variável de ambiente `LD_LIBRARY_PATH` durante a preparação.  Como alternativa, é possível especificar a variável de ambiente `LD_LIBRARY_PATH` no arquivo `manifest.yml` de seu aplicativo ou usando o comando `ibmcloud cf set-env` para usar um nome de pasta
diferente de * ld_library_path *.  Nesse caso, o buildpack anexará esse caminho customizado ao `LD_LIBRARY_PATH` gerado pelo buildpack.
