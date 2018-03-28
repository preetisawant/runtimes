---

copyright:
  years: 2017
lastupdated: "2017-10-26"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Use seu próprio JRE
{: #using_own_jre}

É possível executar o aplicativo Liberty no {{site.data.keyword.Bluemix}} com seu próprio JRE. Deve-se concluir o seguinte para disponibilizar seu JRE para seu aplicativo.
* Hospede o JRE em um local de onde o buildpack possa fazer seu download.
* Hospede um arquivo `index.yml` que fornece o local do JRE.
* Configure seu aplicativo para usar seu JRE.

## Hospede o JRE e o `index.yml`
{: #hosting_jre}

Deve-se hospedar o arquivo JRE em um servidor da web do qual o buildpack do Liberty possa fazer download. É possível hospedar o arquivo no {{site.data.keyword.Bluemix_notm}} com qualquer um dos recursos do servidor disponíveis ou é possível hospedá-lo em um local publicamente disponível. O servidor deve ser configurado com um arquivo `index.yml` que especifique detalhes sobre o arquivo JRE.

Conclua as etapas a seguir para hospedar o JRE e o arquivo `index.yml`:
  1. Adquira o JRE, que deve ser a versão para uso em um S.O. UNIX 64 de bits e deve ser um arquivo `tar.gz`.
  2. Hospede o arquivo JRE em um local a partir do qual o buildpack do Liberty possa fazer download dele.
  3. Forneça um arquivo `index.yml` no local de hospedagem. O arquivo `index.yml` deve incluir uma entrada que contém um ID de versão do JRE seguido por dois-pontos e a URL completa do local do arquivo JRE.
    * Defina a versão JRE no arquivo `index.yml`.

    ```
    ---
   jre_version: https://hostingLocation/jreName.tar.gz
    ```
    {: codeblock}

    * Inclua o ID da versão JRE e o local completo do arquivo JRE.  Por exemplo:

    ```
    ---
       1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```
    {: codeblock}

## Configure o app
{: #configure_app}

Deve-se configurar as variáveis de ambiente no aplicativo Liberty para configurar o buildpack para usar um JRE alternativo. Configure o **JBP_CONFIG_OPENJDK** para identificar o local do arquivo `index.yml` e configure a variável de ambiente **JVM** para *openjdk*. Para obter mais informações sobre o formato para sequências de valor de versão, consulte a documentação do Cloud Foundry no [Sintaxe da versão e ordenação e curingas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/util-repositories.md){: new_window}.

O valor para a variável **JBP_CONFIG_OPENJDK** é o local do arquivo `index.yml` e a versão do JRE da qual escolher o arquivo index.yml.

```
'{repository_root: "https://locationToIndexYml", version: version-value}'
```
{: codeblock}

Emita o comando `cf se myAPP` para configurar a variável **JBP_CONFIG_OPENJDK**, por exemplo:
```
$ cf se myApp JBP_CONFIG_OPENJDK '{repository_root: "https://myHostingApp.ng.bluemix.net", version: 1.8.+}'
```
{: codeblock}

A URL *repository_root* não inclui `index.yml` na URL. A URL *repository_root* aponta para o nível de diretório que contém o arquivo `index.yml`, não o próprio arquivo.

Para configurar a variável de ambiente JVM, emita o comando a seguir:
```
$ cf se myApp JVM 'openjdk'
```
{: codeblock}

**Nota**: remonte seu aplicativo depois de configurar as variáveis de ambiente para que as mudanças entrem em vigor.

## Confirmar
{: #confirmation}

Para confirmar que Liberty está usando o JRE esperado, verifique o log de preparação. Procure uma mensagem que indique que o servidor transferiu por download o buildpack do local indicado no arquivo `index.yml`. Consulte o fragmento a seguir para um exemplo da saída do log quando o Liberty usar com sucesso o JRE esperado.
```
 -----> Downloading OpenJdk 1.8.0_91
from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}
