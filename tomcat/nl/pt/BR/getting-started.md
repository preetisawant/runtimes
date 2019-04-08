---

copyright:
  years: 2017, 2018
lastupdated: "2018-12-05"
subcollection: "Tomcat"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Tutorial Introdução
{: #getting_started}

* {: download} Parabéns, você implementou um aplicativo de amostra Hello World no {{site.data.keyword.Bluemix}}!  Para iniciar, siga este guia passo a passo. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Fazer download de código de amostra)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Fazer download de código do aplicativo" />faça download do código de amostra</a> e explore você mesmo.

Seguindo este tutorial de introdução, você configurará um ambiente de desenvolvimento, implementará um app localmente e no {{site.data.keyword.Bluemix}} e integrará um serviço de banco de dados ao seu app.

Em todos esses docs, as referências à CLI do Cloud Foundry agora foram atualizadas para a CLI do {{site.data.keyword.Bluemix_notm}}! A CLI do {{site.data.keyword.Bluemix_notm}} tem os mesmos comandos conhecidos do Cloud Foundry, mas com uma melhor integração com as contas do {{site.data.keyword.Bluemix_notm}} e outros serviços. Saiba mais sobre como começar a usar a CLI do {{site.data.keyword.Bluemix_notm}} neste tutorial.
{: tip}

## Antes de Começar
{: #prereqs}

Você precisará do seguinte:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/ibmcloud/download_cli.html)
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* [Maven ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat versão 8.0.41 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}


## Etapa 1: clonar o aplicativo de amostra
{: #clone}

Clone o repositório e mude para o diretório no qual o app de amostra está localizado.
  ```
git clone https://github.com/IBM-Cloud/get-iniciado-tomcat
  ```
{: codeblock}

  ```
cd get-started-tomcat
  ```
{: codeblock}

Examine os arquivos no diretório *get-started-tomcat* para familiarizar-se com o conteúdo.

## Etapa 2: executar o app localmente
{: #run_locally}

Deve-se instalar as dependências e construir um arquivo .war conforme definido no arquivo pom.xml para executar o app.

1. Instale as dependências.
  ```
mvn clean install  
  ```
  {: codeblock}

1. Copie GetStartedTomcat.war do diretório `target` para o diretório `tomcat-install-dir` `webapps`.

1. Execute o app.  
  ```
<tomcat-install-dir>/bin/startup.bat|.sh
  ```
  {: codeblock}

1. Visualizar o seu aplicativo na URL a seguir: http://localhost:8080/GetStartedTomcat/

Use `shutdown.bat|.sh` para parar seu app.  Observe que poderá ser necessário fornecer a permissão de execução aos comandos.
{: tip}

## Etapa 3: preparar o app para implementação do {{site.data.keyword.Bluemix_notm}}
{: #prepare}

Para implementar no {{site.data.keyword.Bluemix_notm}}, poderá ser útil configurar um arquivo manifest.yml. O manifest.yml inclui informações básicas sobre seu app, como o nome, quanta memória alocar para cada instância e a rota. Nós fornecemos um arquivo manifest.yml de amostra no diretório `get-started-tomcat`.

Abra o arquivo manifest.yml e mude o `nome` de `GetStartedTomcat` para o nome de seu app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/GetStartedTomcat.war
    buildpack: java_buildpack
  ```
  {: codeblock}

Nesse arquivo manifest.yml, **`random-route: true`** gera uma rota aleatória para seu app para evitar que sua rota colida com outras.  Se você optar por isso, será possível substituir **`random-route: true`** por **`host: myChosenHostName`**, fornecendo um nome de host de sua preferência.
{: tip}

## Etapa 4: implementar o app
{: #deploy}

É possível usar a CLI do {{site.data.keyword.Bluemix_short}} para implementar apps.

1. Efetue login em sua conta do {{site.data.keyword.Bluemix_short}} e selecione um terminal de API.

  ```
ibmcloud login
  ```
  {: codeblock}

  Se você tiver um ID do usuário federado, em vez disso, use o comando a seguir para efetuar login com o seu ID de conexão única. Veja [Efetuando login com um ID federado](/docs/cli/login_federated_id.html) para saber mais.

  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Em seguida, destine a organização e o espaço de um Cloud Foundry:
  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Se você não tiver uma organização nem uma configuração de espaço, veja [Incluindo organizações e espaços](/docs/account/orgs_spaces.html).
  {: tip}

1. De dentro do diretório *get-started-tomcat*, envie o seu aplicativo por push para o {{site.data.keyword.Bluemix_notm}}

  ```
ibmcloud cf push
  ```
  {: codeblock}

  Isso pode levar aproximadamente dois minutos. Se houver um erro no processo de implementação, será possível usar o comando `ibmcloud cf logs <Your-App-Name> --recent` para solucionar problemas.

Quando a implementação for concluída, você deverá ver uma mensagem indicando que o app está em execução.  Visualize o app na URL listada na saída do comando push.  Também é possível emitir o comando a seguir para visualizar o status de seus apps e ver a URL.

  ```
Ibmcloud cf apps
  ```
  {: codeblock}

Também é possível acessar a [Lista de recursos](https://cloud.ibm.com/resources) do {{site.data.keyword.Bluemix_notm}} para visualizar o seu aplicativo.

## Etapa 5: incluir um banco de dados
{: #add_database}

Em seguida, incluiremos um banco de dados NoSQL do {{site.data.keyword.cloudant_short_notm}} nesse aplicativo e configuraremos o aplicativo para que ele possa ser executado localmente e no {{site.data.keyword.Bluemix_notm}}.

1. Em seu navegador, efetue login no {{site.data.keyword.Bluemix_notm}} e acesse o Painel. Selecione **Criar recurso**.
1. Procure **{{site.data.keyword.cloudant_short_notm}}** e selecione o serviço.
1. Para os **Métodos de autenticação disponíveis**, selecione **Usar as credenciais anteriores e o IAM**. É possível deixar as configurações padrão para os outros campos. Clique em **Criar** para criar o serviço.
1. Na navegação, acesse **Conexões** e, em seguida, clique em **Criar conexão**. Selecione o seu aplicativo e clique em **Conectar**.
1. Usando os valores padrão, clique em **Conectar e remontar aplicativo** para conectar o
banco de dados ao seu aplicativo. Clique em **Remontar** quando solicitado.

   O {{site.data.keyword.Bluemix_notm}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_notm}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente referenciada no código-fonte.
{: tip}

## Etapa 6: usar o banco de dados
{: #use_database}

Vamos agora atualizar seu código local para apontar para esse banco de dados. Vamos armazenar as credenciais dos serviços em um arquivo de propriedades. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente `VCAP_SERVICES`.

1. Localize o seu aplicativo na [Lista de recursos](https://cloud.ibm.com/resources) do {{site.data.keyword.Bluemix_notm}}. Na página Detalhes do serviço para o seu aplicativo, clique em **Conexões** na barra lateral. Clique no ícone do menu do {{site.data.keyword.cloudant_short_notm}} (**&hellip;**) e selecione **Visualizar credenciais**.

2. Copie e cole apenas a `URL` das credenciais no campo `URL` do arquivo `cloudant.properties` e salve as mudanças.
  ```
cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:codeblock}

3. Reinicie o servidor

Atualize a visualização do navegador em: http://localhost:8080/GetStartedTomcat/. Os nomes que você inserir no app serão agora incluídos no banco de dados.

  Seu app local e o app {{site.data.keyword.Bluemix_notm}} estão compartilhando o banco de dados. Os nomes que você incluir de qualquer um dos apps aparecerão em ambos quando os navegadores forem atualizados.


Lembre-se, se você não precisar do app em tempo real no {{site.data.keyword.Bluemix_notm}}, pare-o para não incorrer em encargos inesperados.
{: tip}  

## Próximas Etapas

* [Tutorials (Tutoriais)](/docs/tutorials/index.html)
* [Amostras ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
