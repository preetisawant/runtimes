---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-14"

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

Seguindo o tutorial de introdução do Dotnet, você configurará um ambiente de desenvolvimento, implementará um app localmente e no {{site.data.keyword.Bluemix}} e integrará um serviço de banco de dados {{site.data.keyword.Bluemix}} em seu app.

## Antes de Começar
{: #prereqs}

Você precisará do seguinte:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* Instale o .NET Core 1.1 SDK 1.0.4 de acordo com as instruções
do [website do dot.net
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.microsoft.com/net/download/core).

## Etapa 1: clonar o aplicativo de amostra
{: #clone}

Agora você está pronto para começar a trabalhar com o app. Clone o repositório e mude para o diretório no qual o app de amostra está localizado.
  ```
git clone https://github.com/IBM-Bluemix/get-started-aspnet-core
  ```
  {: pre}
  ```
cd get-started-aspnet-core
  ```
  {: pre}

## Etapa 2: executar o app localmente
{: #run_locally}

Execute o app.
  ```
cd src/GetStartedDotnet
  ```
  {: pre}
  ```
dotnet restore
  ```
  {: pre}
  ```
dotnet run
  ```
  {: pre}

Visualize seu app em: http://localhost:5000/

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

Nesse arquivo manifest.yml, **random-route: true** gera uma rota aleatória para seu app para evitar que sua rota colida com outras.  Se você optar por isso, será possível substituir **random-route: true** por **host: myChosenHostName**, fornecendo um nome de host de sua preferência. [Saiba mais...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## Etapa 4: implementar o app
{: #deploy}

É possível usar a CLI do Cloud Foundry para implementar apps.

Para iniciar, efetue login na sua conta do {{site.data.keyword.Bluemix_notm}}:
  ```
cf login
  ```
  {: pre}

  Se não for possível efetuar login usando os comandos `cf login` ou `bx login` porque você tem um ID de usuário federado, use os comandos `cf login --sso` ou `bx login --sso` para efetuar login com seu ID de conexão única. Veja [Efetuando login com um ID federado](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) para saber mais.

Escolha seu terminal de API
  ```
cf api <API-endpoint>
  ```
  {: pre}

Substitua o *API-endpoint* no comando por um terminal de API da lista a seguir.

| **Nome da região** | **Local geográfico** | **Endpoint da API** |
|-----------------|-------------------------|-------------------|
| Região Sul dos EUA | Dallas, EUA | api.ng.bluemix.net |
| Região Leste dos EUA | Washington, DC, EUA | api.us-east.bluemix.net |
| Região do Reino Unido | Londres, Inglaterra | api.eu-gb.bluemix.net |
| Região de Sydney | Sydney, Austrália | api.au-syd.bluemix.net |
| Região da Alemanha | Frankfurt, Alemanha | api.eu-de.bluemix.net |
{: caption="Tabela 1.  {{site.data.keyword.cloud_notm}} lista de região" caption-side="top"}

**Certifique-se de que você esteja no diretório principal, `get-started-aspnet-core`, para seu aplicativo**, em seguida, envie por push seu aplicativo para o {{site.data.keyword.Bluemix_notm}}
  ```
cf push
  ```
  {: pre}

Isso pode levar um minuto. Se houver um erro no processo de implementação, será possível usar o comando `cf logs <Your-App-Name> --recent` para solucionar problemas.

Quando a implementação for concluída, você deverá ver uma mensagem indicando que o app está em execução.  Visualize o app na URL listada na saída do comando push.  Também é possível emitir o comando
  ```
cf apps
  ```
  {: pre}
  para visualizar o status dos apps e ver a URL.

## Etapa 5: conectar um banco de dados MySQL
{: connect_mysql}

Em seguida, vamos incluir um banco de dados ClearDB MySQL para este aplicativo e configurar o aplicativo para que ele possa
ser executado localmente e no {{site.data.keyword.Bluemix_notm}}.

1. Em seu navegador, efetue login no {{site.data.keyword.Bluemix_notm}} e acesse o Painel. Selecione **Criar recurso**.
2. Escolha a seção **Dados e Analytics** e, em seguida, selecione **ClearDB
MySQL** e crie seu serviço.
3. Acesse a visualização **Conexões**, selecione seu aplicativo e, em seguida, **Criar conexão**.
4. Selecione **Remontar** quando solicitado. O {{site.data.keyword.Bluemix_notm}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_notm}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente que seja referenciada em seu código-fonte. [Saiba mais...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Etapa 6: usar o banco de dados localmente
{: #use_database}

Vamos agora atualizar seu código local para apontar para esse banco de dados. Vamos armazenar as credenciais para os serviços em um arquivo json. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente VCAP_SERVICES.

1. Crie o arquivo src/GetStartedDotnet/vcap-local.json

2. Em seu navegador, abra a UI do {{site.data.keyword.Bluemix_notm}}, selecione seu Aplicativo-> Conexões->
Banco de dados ClearDB Managed MySQL-> Visualizar credenciais

3. Copie e cole o objeto json inteiro das credenciais no arquivo `vcap-local.json` e salve as mudanças.  O resultado será algo como:
  ```
  {
  "cleardb": [
    {
      "credentials": {
        ...
        "uri": "mysql://user:password@some-hostname.cleardb.net:3306/database-name?reconnect=true",
        ...
      },
      ...
      "name": "My ClearDB service instance name",
      ...
    }
  ]
}
  ```

4. No diretório `get-started-aspnet-core/src/GetStartedDotnet`, reinicie seu aplicativo com o comando	`dotnet run`.

  Atualize seu navegador em: http://localhost:5000/. Os nomes que você inserir no app serão agora incluídos no banco de dados.

  Seu app local e o app {{site.data.keyword.Bluemix_notm}} estão compartilhando o banco de dados.  Visualize o app {{site.data.keyword.Bluemix_notm}} na URL listada na saída do comando push acima.  Os nomes que você incluir de qualquer um dos apps deverão aparecer em ambos quando os navegadores forem atualizados.

Lembre-se, se você não precisar do app em tempo real, pare-o para não incorrer em encargos inesperados.
{: tip}

## Próximas Etapas

* [Tutorials (Tutoriais)](/docs/tutorials/index.html)
* [Amostras ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
