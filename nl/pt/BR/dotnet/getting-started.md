---

copyright:
  years: 2017, 2019
lastupdated: "2019-03-20"
subcollection: "Dotnet"

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

Seguindo este tutorial de introdução, você configurará um ambiente de desenvolvimento, implementará um aplicativo localmente
e no {{site.data.keyword.Bluemix}} e integrará um serviço de banco de dados do {{site.data.keyword.Bluemix}} em seu
aplicativo.

## Antes de Começar
{: #prereqs}

Você precisará do seguinte:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} CLI](/docs/cli/reference/ibmcloud/download_cli.html)
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* Instale o SDK 2.2.104 do .NET Core 2.2.2 do [Website de downloads do .NET Core ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de linkexterno")](https://www.microsoft.com/net/download/core).


## Etapa 1: clonar o aplicativo de amostra
{: #clone}

Primeiro, clone o repositório GitHub do app de amostra.
  ```
git clone https://github.com/IBM-Cloud/get-iniciado-aspnet-core
  ```
  {: codeblock}


## Etapa 2: executar o app localmente
{: #run_locally}

1. Na linha de comandos, mude o diretório para onde o app de amostra está localizado.

  ```
  cd get-iniciado-aspnet-core/src/GetStartedDotnet
  ```
  {: codeblock}

1. Execute o app localmente executando os comandos a seguir.

  ```
dotnet restore
  ```
  {: codeblock}

  ```
dotnet run
  ```
  {: codeblock}

1. Visualize seu app em: http://localhost: 5000/.

## Etapa 3: preparar o app para implementação
{: #prepare}

Para implementar no {{site.data.keyword.Bluemix_notm}}, poderá ser útil configurar um arquivo manifest.yml. O manifest.yml inclui informações básicas sobre seu app, como o nome, quanta memória alocar para cada instância e a rota. Nós fornecemos um arquivo manifest.yml de amostra no diretório `get-started-dotnet`.

Abra o arquivo manifest.yml e mude o `nome` de `GetStartedDotnet` para o nome de seu app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedDotnet
   random-route: true
   memory: 512M
  ```
  {: codeblock}

Nesse arquivo manifest.yml, **`random-route: true`** gera uma rota aleatória para seu app para evitar que sua rota colida com outras.  Se você optar por isso, será possível substituir **`random-route: true`** por **`host: myChosenHostName`**, fornecendo um nome de host de sua preferência.
{: tip}

## Etapa 4: implementar o app
{: #deploy}

É possível usar a CLI do {{site.data.keyword.Bluemix_notm}} para implementar apps.

1. Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}} e selecione um terminal de API.
  ```
ibmcloud login
  ```
  {: codeblock}

  Se você tiver um ID do usuário federado, em vez disso, use o comando a seguir para efetuar login com o seu ID de conexão única. Veja [Efetuando login com um ID federado](/docs/cli/login_federated_id.html) para saber mais.
 ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Tenha como destino uma organização e um espaço do Cloud Foundry:
  ```
ibmcloud target --cf
  ```
  {: codeblock}

  Se você não tiver uma organização nem uma configuração de espaço, veja [Incluindo organizações e espaços](/docs/account/orgs_spaces.html).
  {: tip}

1. **Certifique-se de estar no diretório principal, `get-started-aspnet-core`, para
o seu aplicativo ** e, então, envie o seu aplicativo por push para o {{site.data.keyword.Bluemix_notm}}:
  ```
ibmcloud cf push
  ```
  {: codeblock}

  Isso pode levar um minuto. Se houver um erro no processo de implementação, será possível usar o comando `ibmcloud cf logs <Your-App-Name> --recent` para solucioná-lo.

Quando a implementação for concluída, será necessário ver uma mensagem indicando que o seu aplicativo está em
execução.  Visualize o app na URL listada na saída do comando push.  Também é possível emitir o comando a seguir para visualizar o status de seu aplicativo e ver a URL.
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

## Etapa 6: usar o banco de dados localmente
{: #use_database}

Vamos agora atualizar seu código local para apontar para esse banco de dados. Nós armazenaremos as credenciais para os
serviços em um arquivo JSON. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente `VCAP_SERVICES`.

1. No diretório `src/GetStartedDotnet`, crie um arquivo `vcap-local.json`.

1. Copie e cole o objeto JSON a seguir no arquivo `vcap-local.json` e salve as mudanças.

   ```json
   {
     "services": {
       "cloudantNoSQLDB": [
        {
           "credentials": {
             "url":"CLOUDANT_DATABASE_URL"
           },
          "label": "cloudantNoSQLDB"
        }
       ]
     }
   }
   ```
   {: codeblock}

1. Localize o seu aplicativo na [Lista de recursos](https://cloud.ibm.com/resources) do {{site.data.keyword.Bluemix_notm}}. Na página Detalhes do serviço para o seu aplicativo, clique em **Conexões** na barra lateral. Clique no ícone do menu do {{site.data.keyword.cloudant_short_notm}} (**&hellip;**) e selecione **Visualizar credenciais**.

1. Copie e cole apenas o valor `url` das credenciais para o campo `url` do arquivo `vcap-local.json`, substituindo `CLOUDANT_DATABASE_URL`.

1. No diretório `get-started-aspnet-core/src/GetStartedDotnet`, reinicie o aplicativo executando o comando a seguir.

   ```
   dotnet run
   ```
   {: codeblock}

1. Atualize a visualização do navegador em http://localhost:5000/. Os nomes que você inserir no app serão agora incluídos no banco de dados.

O aplicativo local e o aplicativo {{site.data.keyword.Bluemix_notm}} compartilham o banco de dados.  Visualize o aplicativo {{site.data.keyword.Bluemix_notm}} na URL listada na saída do comando `ibmcloud cf push`.  Os nomes que você incluir de qualquer um dos apps deverão aparecer em ambos quando os navegadores forem atualizados.

Lembre-se: se você não precisar de seu app em tempo real, pare-o para que você não incorra em nenhum encargo inesperado.
{: tip}

## Próximas Etapas

* [Tutorials (Tutoriais)](/docs/tutorials/index.html)
* [Amostras ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
