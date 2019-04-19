---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-03"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Desenvolva aplicativos usando o IBM Eclipse Tools for {{site.data.keyword.cloud_notm}}

É possível também usar o {{site.data.keyword.eclipsetoolsfull}} como uma maneira alternativa para desenvolver e implementar aplicativos no {{site.data.keyword.Bluemix}}. O {{site.data.keyword.eclipsetoolsfull}} fornece plug-ins que podem ser instalados em um ambiente existente do Eclipse para ajudar na integração de seu ambiente de desenvolvimento integrado (IDE) com o {{site.data.keyword.Bluemix_notm}}.

Esse procedimento segue as mesmas etapas gerais que o [Tutorial de introdução](getting-started.html) para o Liberty. Usando o Eclipse, você irá configurar um ambiente de desenvolvimento, implementará um aplicativo localmente e na nuvem e integrará
um serviço de banco de dados {{site.data.keyword.Bluemix_notm}} em seu aplicativo.

## Antes de Começar
{: #prereqs}

Você precisará das contas e ferramentas a seguir:
* [IBM Eclipse Tools for IBM Cloud ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}
* [Eclipse IDE for Java EE Developers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}

Se você concluiu o [Tutorial de introdução](getting-started.md), você pode já ter essas ferramentas e contas. Tenha certeza de ter os seguintes itens instalados e registrados antes de iniciar:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/registration)
* [{{site.data.keyword.Bluemix_notm}} CLI](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* [Maven ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://maven.apache.org/download.cgi){: new_window}

## Etapa 1: clonar o aplicativo de amostra
{: #clone}

Primeiro, clone o repositório GitHub do app de amostra.

  ```
git clone https://github.com/IBM-Cloud/get-started-java
  ```
  {: codeblock}

## Etapa 2: compilar seu código-fonte do aplicativo
{: #build_app}

Use Maven para construir seu código-fonte e execute o app resultante.

1. Na linha de comandos, mude o diretório para onde o app de amostra está localizado.

  ```
cd get-started-java
  ```
  {: codeblock}

1. Use Maven para instalar as dependências e construir o arquivo .war.

  ```
mvn clean install
  ```
  {: codeblock}

## Etapa 3: preparar o app para implementação
{: #prepare}

Para implementar no {{site.data.keyword.Bluemix_notm}}, poderá ser útil configurar um arquivo manifest.yml. O manifest.yml inclui informações básicas sobre seu app, como o nome, quanta memória alocar para cada instância e a rota. Nós fornecemos um arquivo manifest.yml de amostra no diretório `get-started-java`.

Abra o arquivo manifest.yml e mude o `nome` de `GetStartedJava` para o nome de seu app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

Nesse arquivo manifest.yml, **random-route: true** gera uma rota aleatória para seu app para evitar que sua rota colida com outras.  Se você optar por isso, será possível substituir **random-route: true** por **host: myChosenHostName**, fornecendo um nome de host de sua preferência.
{: tip}

## Etapa 4: Efetuar login no {{site.data.keyword.Bluemix_notm}}
{: #deploy}

1. Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}} e selecione um terminal de API.

  ```
ibmcloud login
  ```
  {: codeblock}

  Se não for possível efetuar login usando `ibmcloud login` porque você tem um ID do usuário federado, use o seguinte para efetuar login com o seu ID de conexão única. Veja [Efetuando login com um ID federado](https://cloud.ibm.com/docs/iam?topic=iam-federated_id#federated_id) para saber mais.

  ```
ibmcloud login --sso
  ```
  {: codeblock}

  Em seguida, tenha como destino a CLI do Cloud Foundry:

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Se você não tiver uma organização nem uma configuração de espaço, veja [Incluindo organizações e espaços](https://cloud.ibm.com/docs/account?topic=account-orgsspacesusers#orgsspacesusers).
  {: tip}

## Etapa 5: desenvolver usando o Eclipse
{: #eclipse}

1. Certifique-se de que tenha o [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix).

2. Importe a amostra `get-started-java` para o Eclipse acessando **Arquivo > Importar > Maven > Projetos existentes do Maven**.

3. Crie uma definição de servidor Liberty. As etapas a seguir farão download de um novo servidor Liberty.
  - Na visualização **Janela > Mostrar visualização > Servidores**, clique com o botão direito e selecione **Novo > Servidor**.
  - Selecione **IBM > WebSphere Application Server Liberty**.
  - Selecione **Instalar de um archive ou um repositório**.
  - Quando solicitado, insira um caminho de destino em uma nova pasta (/Users/username/liberty) na qual você deseja instalar o Liberty.
  - Selecione **Fazer download e instalar um novo ambiente de tempo de execução do ibm.com**.
  - Selecione **WAS Liberty com Java EE 7 Web Profile**.
  - Continue o assistente com opções padrão para concluir.

4. Execute seu aplicativo localmente no Liberty.
  - Mude o navegador da web para o padrão do sistema acessando **Janela > Navegador da web > navegador da web do sistema padrão**.
  - Clique com o botão direito na amostra `GetStartedJava` e selecione **Executar como > Executar no servidor**.
  - Localize e selecione o servidor Liberty localhost e clique em **Concluir**.

  Em alguns segundos, seu aplicativo estará em execução em http://localhost:9080/GetStartedJava.

5. Atualize o código:
  - Abra `src/main/webapp/index.html` e atualize o título de `<h1>Bem-vindo.</h1>` para `<h1>Bem-vindo Jane.</h1>`.
  - Salve suas mudanças. O Liberty assimilará suas mudanças automaticamente.
  - Atualize seu navegador (http://localhost:9080/GetStartedJava) para ver as mudanças.

6. Envie suas mudanças por push para o {{site.data.keyword.Bluemix_notm}}:
  - No diretório `get-started-java`, na linha de comandos, reconstrua o arquivo .war.

    ```
mvn clean install
    ```
    {: codeblock}

  - Envie seu aplicativo por push para {{site.data.keyword.Bluemix_notm}}.

    ```
ibmcloud cf push
    ```
    {: codeblock}

Agora você executou seu código localmente e na nuvem!

## Etapa 6: incluir um banco de dados
{: #add_database}

Em seguida, vamos incluir um banco de dados NoSQL nesse aplicativo e configurar o aplicativo para que ele possa ser executado localmente e no {{site.data.keyword.Bluemix_notm}}.

1. Em seu navegador, efetue login no {{site.data.keyword.Bluemix_notm}} e acesse o Painel. Selecione **Criar recurso**.
2. Escolha a seção **Dados e análise de dados**, selecione o **{{site.data.keyword.cloudant_short_notm}}** e crie o seu serviço.
3. Acesse a visualização **Conexões**, selecione seu aplicativo e, em seguida, **Criar conexão**.
4. Selecione **Remontar** quando solicitado. O {{site.data.keyword.Bluemix_notm}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_notm}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente que seja referenciada em seu código-fonte.
{: tip}

## Etapa 7: usar o banco de dados
{: #use_database}
Vamos agora atualizar seu código local para apontar para esse banco de dados. Vamos armazenar as credenciais dos serviços em um arquivo de propriedades. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente `VCAP_SERVICES`.

1. No Eclipse, abra o arquivo src/main/resources/cloudant.properties:

  ```
  cloudant_url=
  ```
  {: codeblock}

2. Em seu navegador, acesse {{site.data.keyword.Bluemix_notm}} e selecione **Apps > _seu app_ > Conexões > Cloudant > Visualizar credenciais**.

3. Copie e cole apenas a `URL` das credenciais no campo `URL` do arquivo `cloudant.properties` e salve as mudanças.

  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:codeblock}

4. Reinicie o servidor Liberty no Eclipse por meio da visualização `Servidores`.

  Atualize seu navegador em http://localhost:9080/GetStartedJava/. Os nomes que você inserir no app serão agora incluídos no banco de dados.

  Seu app local e o app {{site.data.keyword.Bluemix_notm}} estão compartilhando o banco de dados. Os nomes que você incluir de qualquer um dos apps aparecerão em ambos quando os navegadores forem atualizados.


Lembre-se, se você não precisar do app em tempo real no {{site.data.keyword.Bluemix_notm}}, pare-o para não incorrer em encargos inesperados.
{: tip}  
