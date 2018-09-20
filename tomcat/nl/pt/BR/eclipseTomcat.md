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

# Desenvolva aplicativos Tomcat usando o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}

É possível também usar o {{site.data.keyword.eclipsetoolsfull}} como uma maneira alternativa para desenvolver e implementar aplicativos no {{site.data.keyword.Bluemix}}. O IBM Eclipse Tools fornece plug-ins que podem ser instalados em um ambiente Eclipse existente para ajudar na integração de seu ambiente de desenvolvimento integrado (IDE) com {{site.data.keyword.Bluemix_notm}}.

Esse procedimento segue as mesmas etapas gerais que o [Tutorial de introdução](getting-started.html) para o Liberty. Usando o Eclipse, você irá configurar um ambiente de desenvolvimento, implementará um aplicativo localmente e na nuvem e integrará um serviço de banco de dados em seu aplicativo.

## Antes de Começar
{: #prereqs}

Você precisará das contas e ferramentas a seguir:
* [IBM Eclipse Tools for IBM Cloud ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}
* [Eclipse IDE for Java EE Developers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}

Se você concluiu o [Tutorial de introdução](getting-started.md), você pode já ter essas ferramentas e contas. Tenha certeza de ter os seguintes itens instalados e registrados antes de iniciar:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} CLI](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* [Maven ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat versão 8.0.41 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}

## Etapa 1: clonar o aplicativo de amostra
{: #clone}

Primeiro, clone o repositório GitHub do app de amostra.

  ```
git clone https://github.com/IBM-Cloud/get-iniciado-tomcat
  ```
  {: codeblock}

## Etapa 2: compilar seu código-fonte do aplicativo
{: #build_app}

Use Maven para construir seu código-fonte e execute o app resultante.

1. Na linha de comandos, mude o diretório para onde o app de amostra está localizado.

  ```
cd get-started-tomcat
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
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/GetStartedTomcat.war
    buildpack: java_buildpack
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

  Se não for possível efetuar login usando `ibmcloud login` porque você tem um ID do usuário federado, use o seguinte para efetuar login com o seu ID de conexão única. Veja [Efetuando login com um ID federado](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) para saber mais.
  ```
ibmcloud login --sso
  ```
  {: codeblock}

  Em seguida, tenha como destino a CLI do Cloud Foundry:
  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Se você não tiver uma organização nem uma configuração de espaço, veja [Incluindo organizações e espaços](https://console.bluemix.net/docs/account/orgs_spaces.html).
  {: tip}

## Etapa 5: desenvolver usando o Eclipse
{: #eclipse}

1. Certifique-se de que você tenha o [IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix).

2. Importe a amostra `get-started-java` para o Eclipse acessando **Arquivo > Importar > Maven > Projetos existentes do Maven**.

3. Crie uma definição de servidor Tomcat:
  - Na visualização **Servidores**, clique com o botão direito e selecione **Novo> Servidor**.
  - Selecione  ** Apache > Servidor Tomcat v8.0 **.
  - Escolha o `tomcat-install-dir`.
  - Continue o assistente com opções padrão para concluir.

4. Execute seu aplicativo localmente no servidor Apache.
  - Clique com o botão direito na amostra `GetStartedTomcat` e selecione **Executar como > Executar
no servidor**.
  - Localize e selecione o servidor Tomcat do host local e clique em **Concluir**.
  - Em alguns segundos, o seu aplicativo estará em execução em http://localhost:8080/GetStartedTomcat/

5. Execute seu aplicativo no {{site.data.keyword.Bluemix_notm}}:
  - Clique com o botão direito na amostra `GetStartedTomcat` e selecione **Executar como > Executar
no servidor**.
  - Localize e selecione **{{site.data.keyword.Bluemix_notm}}** e, em seguida, clique em **Concluir**.
  - Um assistente fornecerá instruções com as opções de implementação. Certifique-se de escolher um `Nome` exclusivo para seu aplicativo.
  - Em alguns minutos, o seu aplicativo estará em execução na URL que você escolher.

Agora você executou seu código localmente e na nuvem!

## Etapa 6: incluir um banco de dados
{: #add_database}

Em seguida, vamos incluir um banco de dados {{site.data.keyword.cloudantfull}} para este aplicativo e configurar o aplicativo para que ele possa ser executado localmente e no {{site.data.keyword.Bluemix_notm}}.

1. Em seu navegador, efetue login no {{site.data.keyword.Bluemix_notm}} e acesse o Painel. Selecione **Criar recurso**.
2. Escolha a seção **Dados e análise de dados**, selecione o **{{site.data.keyword.cloudant_short_notm}}** e crie o seu serviço.
3. Acesse a visualização **Conexões**, selecione seu aplicativo e, em seguida, **Criar conexão**.
4. Selecione **Remontar** quando solicitado. O {{site.data.keyword.Bluemix_notm}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_notm}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente que seja referenciada em seu código-fonte.
{: tip}

## Etapa 7: usar o banco de dados
{: #use_database}
Vamos agora atualizar seu código local para apontar para esse banco de dados. Vamos armazenar as credenciais dos serviços em um arquivo de propriedades. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente VCAP_SERVICES.

1. Abra o Eclipse e o arquivo src/main/resources/cloudant.properties:

  ```
  cloudant_url=
  ```
  {: codeblock}

2. Em seu navegador, abra a UI do {{site.data.keyword.Bluemix_notm}}, selecione seu App -> Conexões -> Cloudant -> Visualizar credenciais

3. Copie e cole apenas a `URL` das credenciais no campo `URL` do arquivo `cloudant.properties` e salve as mudanças.  O resultado será algo como:

  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {: codeblock}

4. Reinicie o servidor Tomcat no Eclipse por meio da visualização `Servidores`.

  Atualize a visualização do navegador em: http://localhost:8080/GetStartedTomcat/. Os nomes que você inserir no app serão agora incluídos no banco de dados.

  Seu app local e o app {{site.data.keyword.Bluemix_notm}} estão compartilhando o banco de dados.  Visualize o app {{site.data.keyword.Bluemix_notm}} na URL listada na saída do comando push acima.  Os nomes que você incluir de qualquer um dos apps deverão aparecer em ambos quando os navegadores forem atualizados.

Lembre-se, se você não precisar do app em tempo real no {{site.data.keyword.Bluemix_notm}}, pare-o para não incorrer em encargos inesperados.
{: tip}
