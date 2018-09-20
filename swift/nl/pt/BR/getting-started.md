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

# Tutorial Introdução

* {: download} Parabéns, você implementou um aplicativo de amostra Hello World no {{site.data.keyword.Bluemix}}!  Para iniciar, siga este guia passo a passo. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Fazer download de código de amostra)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Fazer download de código do aplicativo" />faça download do código de amostra</a> e explore você mesmo.

Seguindo este tutorial, você configurará um ambiente de desenvolvimento, implementará um app localmente e no {{site.data.keyword.Bluemix}} e integrará um serviço de banco de dados do {{site.data.keyword.Bluemix_notm}} ao seu app.

Em todos esses docs, as referências à CLI do Cloud Foundry agora foram atualizadas para a CLI do {{site.data.keyword.Bluemix_notm}}! A CLI do {{site.data.keyword.Bluemix_notm}} tem os mesmos comandos conhecidos do Cloud Foundry, mas com uma melhor integração com as contas do {{site.data.keyword.Bluemix_notm}} e outros serviços. Saiba mais sobre como começar a usar a CLI do {{site.data.keyword.Bluemix_notm}} neste tutorial.
{: tip}

## Antes de Começar
{: #prereqs}
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* [{{site.data.keyword.Bluemix_notm}} CLI](../../cli/reference/bluemix_cli/download_cli.html)
* [Compilador Swift ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://swift.org/download/) de sua plataforma.

## Etapa 1: clonar o aplicativo de amostra
{: #clone}

Primeiro, clone o repositório e mude para o diretório no qual o aplicativo de amostra está localizado.
  ```
git clone https://github.com/IBM-Cloud/get-iniciado-swift
  ```
  {: codeblock}

  ```
cd get-started-swift
  ```
  {: codeblock}

  Examine os arquivos no diretório *get-started-swift* para familiarizar-se com o conteúdo.

## Etapa 2: executar o app localmente
{: #run_locally}

Depois de ter instalado o compilador Swift e clonado esse repositório Git, será possível agora compilar e executar o aplicativo.

1. Acesse o diretório-raiz desse repositório em seu sistema e emita o comando a seguir:

  ```
swift build
  ```
  {: codeblock}

  Esse comando pode levar alguns minutos para ser executado.

1. Quando o aplicativo for compilado com êxito, será possível executar o executável que foi gerado pelo compilador Swift:
```
swift run
```
  {: codeblock}

  ou
  ```
.build/debug/get-started-swift
  ```
  {: codeblock}

  Você deve ver uma saída semelhante à seguinte:

  ```
Server is listening on port: 8080
  ```
  {: pre}

1. Visualize o seu app na URL a seguir: http://localhost:8080

## Etapa 3: preparar o app para implementação
{: #prepare}

Para implementar no {{site.data.keyword.Bluemix_short}}, poderá ser útil configurar um arquivo manifest.yml. O manifest.yml inclui informações básicas sobre seu app, como o nome, quanta memória alocar para cada instância e a rota. Nós fornecemos um arquivo manifest.yml de amostra no diretório `get-started-swift`.

Abra o arquivo manifest.yml e mude o `nome` de `GetStartedSwift` para o nome de seu app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: Get-Started-Swift
     random-route: true
     memory: 256M
     command: get-started-swift
     buildpack: swift_buildpack
  ```
  {: codeblock}

Nesse arquivo manifest.yml, **random-route: true** gera uma rota aleatória para seu app para evitar que sua rota colida com outras.  Se você optar por isso, será possível substituir **random-route: true** por **host: myChosenHostName**, fornecendo um nome de host de sua preferência.
{: tip}

## Etapa 4: implementar o app
{: #deploy}

É possível usar a CLI do {{site.data.keyword.Bluemix_short}} para implementar apps.

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

1. De dentro do diretório *get-started-swift*, envie o seu aplicativo por push para o {{site.data.keyword.Bluemix_notm}}
  ```
ibmcloud cf push
  ```
  {: codeblock}

  Isso pode levar um minuto. Se houver um erro no processo de implementação, será possível usar o comando `ibmcloud cf logs <Your-App-Name> --recent` para solucionar problemas.

Quando a implementação for concluída, você deverá ver uma mensagem indicando que o app está em execução.  Visualize o app na URL listada na saída do comando push.  Também é possível emitir o comando a seguir para visualizar o status de seus apps e ver a URL.
  ```
Ibmcloud cf apps
  ```
  {: codeblock}

## Etapa 5: incluir um banco de dados
{: #add_database}

Em seguida, incluiremos um banco de dados do {{site.data.keyword.cloudant_short_notm}} nesse aplicativo e configuraremos o aplicativo para que ele possa ser executado localmente e no {{site.data.keyword.Bluemix_notm}}.

1. Em seu navegador, efetue login no {{site.data.keyword.Bluemix_notm}} e acesse o Painel. Selecione **Criar recurso**.
2. Escolha a seção **Dados e análise de dados**, selecione o **{{site.data.keyword.cloudant_short_notm}}** e crie o seu serviço.
3. Acesse a visualização **Conexões**, selecione seu aplicativo e, em seguida, **Criar conexão**.
4. Selecione **Remontar** quando solicitado. O {{site.data.keyword.Bluemix_notm}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_notm}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente que seja referenciada em seu código-fonte.
{: tip}

## Etapa 6: usar o banco de dados
{: #use_database}

Vamos agora atualizar seu código local para apontar para esse banco de dados. Crie um arquivo JSON que armazenará as
credenciais para os serviços que o aplicativo usará. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente VCAP_SERVICES.

Crie um arquivo chamado `my-cloudant-credentials.json` no diretório `config` com o
conteúdo a seguir (como referência, consulte `config/my-cloudant-credentials.json.example`):

 ```
 {
   "password": "<password>",
   "url": "<url>",
   "username": "<username>"
 }
 ```
 {: codeblock}

Atualize o arquivo `mappings.json` no diretório `config` substituindo o
item temporário `cloudant` pelo **nome** de sua instância do banco de dados:

  ```
{
  "MyCloudantDB": {
    "searchPatterns": [
      "cloudfoundry:cloudant",
      "env:kube-cloudant-credentials",
      "file:config/my-cloudant-credentials.json"
    ]
  }
}
  ```
  {: codeblock}

Esse aplicativo de amostra usa o pacote `CloudEnvironment` para interagir com o {{site.data.keyword.Bluemix_notm}}
para analisar as variáveis de ambiente. [Saiba mais...](https://github.com/IBM-Swift/CloudEnvironment)

O item temporário `cloudant` na configuração `cloudfoundry:cloudant` torna mais
fácil ligar um serviço Cloudant fornecido pelo usuário ao seu aplicativo. Com a configuração
`cloudfoundry:cloudant`, é possível criar um serviço Cloudant que inclui a sequência,
`cloudant` em algum lugar no nome do serviço e liga-o ao seu aplicativo, sem editar o arquivo `config.json`. Se você modificar essa configuração e depois quiser usar um serviço Cloudant fornecido pelo usuário, será necessário editar a
configuração para `cloudfoundry:cloudant` ou definir `cloudfoundry:` com o nome do seu
serviço fornecido pelo usuário.
{: tip}

Em seu navegador, acesse o painel do {{site.data.keyword.Bluemix_notm}} e selecione **_seu app_ > Conexões**. Clique no ícone do menu do {{site.data.keyword.cloudant_short_notm}} (**&vellip;**) e selecione **Visualizar credenciais**.

Copie e cole apenas as credenciais para os campos correspondentes em seu arquivo config.json local.

Construa e execute o aplicativo localmente.
 ```
swift build  
 ```
 {: codeblock}

  ```
.build/debug/kitura-helloworld
  ```
 {: codeblock}

 Visualize seu app em: http://localhost:8080. Os nomes que você inserir no app serão agora incluídos no banco de dados.

 Esse aplicativo de amostra usa o pacote `Kitura-CouchDB` para interagir com o Cloudant. [Saiba mais...](https://github.com/IBM-Swift/Kitura-CouchDB)

 Faça quaisquer mudanças desejadas e reimplemente para {{site.data.keyword.Bluemix_notm}}!

  ```
ibmcloud cf app push
  ```

Visualize o seu aplicativo na URL listada na saída do comando push, por exemplo, *myUrl.mybluemix.net*.

Lembre-se: se você não precisar de seu app em tempo real, pare-o para que você não incorra em nenhum encargo inesperado.
{: tip}

## Próximas Etapas

* [Tutoriais do Swift do lado do servidor e do Kitura ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.kitura.io/learn.html){: new_window}
* [Amostras ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
