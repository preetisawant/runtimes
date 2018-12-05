---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-24"
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
{: #getting-started}

* {: download} Parabéns, você implementou um aplicativo de amostra Hello World no {{site.data.keyword.Bluemix}}!  Para iniciar, siga este guia passo a passo. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Fazer download de código de amostra)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Fazer download de código do aplicativo" />faça download do código de amostra</a> e explore você mesmo.

Seguindo este tutorial, você configurará um ambiente de desenvolvimento, implementará um app localmente e no {{site.data.keyword.Bluemix}} e integrará um serviço de banco de dados do {{site.data.keyword.Bluemix_notm}} ao seu app.

Em todos esses docs, as referências à CLI do Cloud Foundry agora foram atualizadas para a CLI do {{site.data.keyword.Bluemix_notm}}! A CLI do {{site.data.keyword.Bluemix_notm}} tem os mesmos comandos conhecidos do Cloud Foundry, mas com uma melhor integração com as contas do {{site.data.keyword.Bluemix_notm}} e outros serviços. Saiba mais sobre como começar a usar a CLI do {{site.data.keyword.Bluemix_notm}} neste tutorial.
{: tip}

## Antes de Começar
{: #prereqs}

Você precisará das contas e ferramentas a seguir:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/registration/)
* [{{site.data.keyword.Bluemix_notm}} CLI](../../cli/reference/bluemix_cli/download_cli.html)
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* [Nó ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://nodejs.org/en/){: new_window}


## Etapa 1: clonar o aplicativo de amostra
{: #clone}

Primeiro, clone o repositório GitHub do app de amostra Node.js *hello world*.
  ```
git clone https://github.com/IBM-Cloud/get-iniciado-node
  ```
  {: codeblock}

## Etapa 2: executar o app localmente
{: #run_locally}

Use o gerenciador de pacote npm para instalar dependências e executar seu app.

1. Na linha de comandos, mude o diretório para onde o app de amostra está localizado.
  ```
cd get-started-node
  ```
  {: codeblock}

1. Instale as dependências listadas no arquivo [package.json ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.npmjs.com/files/package.json) para executar o app localmente.  
  ```
npm install
  ```
  {: codeblock}

1. Execute o app.
  ```
npm start  
  ```
  {: codeblock}

1. Visualize o seu app na URL a seguir: http://localhost:3000

Use [nodemon](https://nodemon.io/) para reinicialização automática do aplicativo em mudanças no arquivo.
{: tip}

## Etapa 3: preparar o app para implementação
{: #prepare}

Para implementar no {{site.data.keyword.Bluemix_notm}}, poderá ser útil configurar um arquivo manifest.yml. O manifest.yml inclui informações básicas sobre seu app, como o nome, quanta memória alocar para cada instância e a rota. Nós fornecemos um arquivo manifest.yml de amostra no diretório `get-started-node`.

Abra o arquivo manifest.yml e mude o `nome` de `GetStartedNode` para o nome de seu app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

```
applications:
- name: GetStartedNode
  random-route: true
  memory: 128M
```
{: codeblock}

Nesse arquivo manifest.yml, **random-route: true** gera uma rota aleatória para seu app para evitar que sua rota colida com outras.  Se você optar por isso, será possível substituir **random-route: true** por **host: myChosenHostName**, fornecendo um nome de host de sua preferência.
{: tip}

## Etapa 4: implementar o app
{: #deploy}

É possível usar a CLI do {{site.data.keyword.Bluemix_notm}} para implementar aplicativos no {{site.data.keyword.Bluemix_notm}}.

1. Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}} e selecione um terminal de API.
  ```
ibmcloud login
  ```
  {: codeblock}

  Se você tiver um ID do usuário federado, em vez disso, use o comando a seguir para efetuar login com o seu ID de conexão única. Veja [Efetuando login com um ID federado](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) para saber mais.
  ```
ibmcloud login --sso
  ```
  {: codeblock}

1. Tenha como destino uma organização e um espaço do Cloud Foundry:

  ```	  
ibmcloud target --cf
  ```
  {: codeblock}

  Se você não tiver uma organização nem uma configuração de espaço, veja [Incluindo organizações e espaços](https://console.bluemix.net/docs/account/orgs_spaces.html).
    {: tip}

1. No diretório *get-started-node*, envie seu app por push para o {{site.data.keyword.Bluemix_notm}}.

  ```
ibmcloud cf push
  ```
  {: codeblock}

A implementação de seu aplicativo pode levar alguns minutos. Quando a implementação for concluída, você verá uma mensagem informando que o app está em execução. Visualize o app na URL listada na saída do comando push ou visualize o status de implementação do app e a URL, executando o comando a seguir:

  ```
Ibmcloud cf apps
  ```
  {: codeblock}

É possível solucionar problemas de erros no processo de implementação usando os `ibmcloud cf logs <Your-App-Name> --recent`.
{: tip}

## Etapa 5: incluir um banco de dados
{: #add_database}

Em seguida, incluiremos um banco de dados NoSQL do {{site.data.keyword.cloudant_short_notm}} nesse aplicativo e configuraremos o aplicativo para que ele possa ser executado localmente e no {{site.data.keyword.Bluemix_notm}}.

1. Em seu navegador, efetue login no {{site.data.keyword.Bluemix_notm}} e acesse o Painel. Selecione **Criar recurso**.
1. Procure **{{site.data.keyword.cloudant_short_notm}}** e selecione o serviço.
1. Para os **Métodos de autenticação disponíveis**, selecione **Usar as credenciais anteriores e o IAM**. É possível deixar as configurações padrão para os outros campos. Clique em **Criar** para criar o serviço.
1. Na navegação, acesse **Conexões**. Selecione seu aplicativo e clique em **Criar conexão**.
1. Conecte-se ao seu aplicativo usando os valores padrão e clique em **Conectar e remontar app**. Em seguida, clique em **Remontar** quando for solicitado.

   O {{site.data.keyword.Bluemix_notm}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_notm}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente referenciada no código-fonte.
{: tip}

## Etapa 6: usar o banco de dados
{: #use_database}
Vamos agora atualizar seu código local para apontar para esse banco de dados. Criaremos um arquivo JSON que armazenará as credenciais dos serviços que o aplicativo usará. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente `VCAP_SERVICES`.

1. No diretório `get-started-node`, crie um arquivo chamado `vcap-local.json` com o conteúdo a seguir:
  ```
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

2. Em seu navegador, acesse o painel do {{site.data.keyword.Bluemix_notm}} e selecione **_seu app_ > Conexões**. Clique no ícone do menu do {{site.data.keyword.cloudant_short_notm}} (**&vellip;**) e selecione **Visualizar credenciais**.

3. Copie e cole apenas a `url` das credenciais para o campo `url` do arquivo `vcap-local.json`, substituindo `CLOUDANT_DATABASE_URL`.

4. Execute seu aplicativo localmente.
  ```
npm start  
  ```
  {: codeblock}

  Visualize seu app local em http://localhost:3000. Os nomes que você inserir no app serão agora incluídos no banco de dados.

** Evite problemas**: o {{site.data.keyword.Bluemix_notm}} define a variável de ambiente PORT
quando seu aplicativo é executado na nuvem. Ao executar seu aplicativo localmente, a variável PORT não é definida, então, 3000 é
usado como o número da porta. Consulte [Execute seu aplicativo localmente](runningLocally.html#hints) para obter
informações adicionais.

  Seu app local e o app {{site.data.keyword.Bluemix_notm}} estão compartilhando o banco de dados. Os nomes que você incluir de qualquer um dos apps aparecerão em ambos quando os navegadores forem atualizados.

Lembre-se, se você não precisar do app em tempo real no {{site.data.keyword.Bluemix_notm}}, pare-o para não incorrer em encargos inesperados.
{: tip}

## Próximas Etapas

* [Tutorials (Tutoriais)](/docs/tutorials/index.html)
* [Amostras ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
