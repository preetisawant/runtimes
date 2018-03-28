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

* {: download} Parabéns, você implementou um aplicativo de amostra Hello World no {{site.data.keyword.Bluemix}}!  Para iniciar, siga este guia passo a passo. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Fazer download de código de amostra)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Fazer download de código do aplicativo" />faça download do código de amostra</a> e explore você mesmo.

Seguindo o tutorial de introdução, você irá configurar um ambiente de desenvolvimento, implementará um app localmente e no
{{site.data.keyword.Bluemix}} e integrar um serviço de banco de dados {{site.data.keyword.Bluemix_notm}} em seu
aplicativo.

## Antes de Começar
{: #prereqs}

Você precisará do seguinte:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* [Go ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://golang.org/dl/){: new_window}

## Etapa 1: clonar o aplicativo de amostra
{: #clone}

Primeiro vamos configurar o ambiente local, assegurando que todas as variáveis de ambiente GO sejam configuradas adequadamente. Por exemplo:
```
mkdir $HOME/work
export GOPATH=$HOME/work
export PATH=$PATH:$GOPATH/bin
```

Mude o caminho para $GOPATH/src
```
mkdir $GOPATH/src
cd $GOPATH/src
```

Agora você está pronto para começar a trabalhar com o app simples *hello world* de Go. Clone o repositório e mude para o diretório no qual o app de amostra está localizado.
```
go get github.com/IBM-Bluemix/get-started-go
```
{: pre}
```
cd github.com/IBM-Bluemix/get-started-go
```
{: pre}

Examine os arquivos no diretório *get-started-go* para familiarizar-se com o conteúdo.

## Etapa 2: executar o app localmente
{: #run_locally}

  {: pre}

  Construa e execute o app.
  ```
make
  ```
  {: pre}

  ```
go run main.go
  ```
  {: pre}

  Visualize seu app em: http://localhost:8080

Use *Ctrl-c* para parar o app na mesma janela em que o app foi iniciado.
{: tip}

## Etapa 3: preparar o app para implementação
{: #prepare}

Para implementar no {{site.data.keyword.Bluemix_notm}}, poderá ser útil configurar um arquivo manifest.yml. O manifest.yml inclui informações básicas sobre seu app, como o nome, quanta memória alocar para cada instância e a rota. Nós fornecemos um arquivo manifest.yml de amostra no diretório `get-started-go`.

Abra o arquivo manifest.yml e mude o `nome` de `GetStartedGo` para o nome de seu app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedGo
   random-route: true
   memory: 128M
   buildpack: go_buildpack
  ```
  {: codeblock}

Nesse arquivo manifest.yml, **random-route: true** gera uma rota aleatória para seu app para evitar que sua rota colida com outras.  Se você optar por isso, será possível substituir **random-route: true** por **host: myChosenHostName**, fornecendo um nome de host de sua preferência. [Saiba mais...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## Etapa 4: implementar o app
{: #deploy}
É possível usar a CLI do Cloud Foundry para implementar apps.

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

Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}}.

  ```
cf login
  ```
  {: pre}

Se não for possível efetuar login usando os comandos `cf login` ou `bx login` porque você tem um ID de usuário federado, use os comandos `cf login --sso` ou `bx login --sso` para efetuar login com seu ID de conexão única. Veja [Efetuando login com um ID federado](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) para saber mais.

No diretório *get-started-go*, envie seu app por push para o {{site.data.keyword.Bluemix_notm}}
  ```
cf push
  ```
  {: pre}

Isso pode levar um minuto. Se houver um erro no processo de implementação, será possível usar o comando `cf logs <Your-App-Name> --recent` para solucionar problemas.

Quando a implementação for concluída, você deverá ver uma mensagem indicando que o app está em execução.  Visualize o app na URL listada na saída do comando push. Também é possível emitir o comando

   ```
cf apps
    ```
  {: pre}
para visualizar o status dos apps e ver a URL.

## Etapa 5: incluir um banco de dados
{: #add_database}

Em seguida, vamos incluir um banco de dados NoSQL nesse aplicativo e configurar o aplicativo para que ele possa ser executado localmente e no {{site.data.keyword.Bluemix_notm}}.

1. Em seu navegador, efetue login no {{site.data.keyword.Bluemix_notm}} e acesse o Painel. Selecione **Criar recurso**.
2. Escolha a seção **Dados e análise de dados**, selecione **Cloudant NoSQL DB** e crie seu serviço.
3. Acesse a visualização **Conexões**, selecione seu aplicativo e, em seguida, **Criar conexão**.
4. Selecione **Remontar** quando solicitado. O {{site.data.keyword.Bluemix_notm}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_notm}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente que seja referenciada em seu código-fonte. [Saiba mais...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Etapa 6: usar o banco de dados
{: #use_database}
Vamos agora atualizar seu código local para apontar para esse banco de dados. Criaremos um arquivo json que armazenará as credenciais dos serviços que o aplicativo usará. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente VCAP_SERVICES.

1. Crie um arquivo chamado `.env` no diretório `get-started-go` com o conteúdo a seguir:
  ```
  CLOUDANT_URL=
  ```
  {: pre}

2. De volta na UI do {{site.data.keyword.Bluemix_notm}}, selecione seu App -> Conexões -> Cloudant -> Visualizar credenciais

3. Copie e cole apenas a `URL` das credenciais no campo `CLOUDANT_URL` do arquivo `.env` e salve as mudanças.  O resultado será algo como:
  ```
  CLOUDANT_URL=https://123456789 ... bluemix.cloudant.com
  ```

4. Execute seu aplicativo localmente.
  ```
go run main.go
  ```
  {: pre}

  Visualize seu app em: http://localhost:8080. Os nomes que você inserir no app serão agora incluídos no banco de dados.

  Seu app local e o app {{site.data.keyword.Bluemix_notm}} estão compartilhando o banco de dados.  Visualize o app {{site.data.keyword.Bluemix_notm}} na URL listada na saída do comando push acima.  Os nomes que você incluir de qualquer um dos apps deverão aparecer em ambos quando os navegadores forem atualizados.


Lembre-se, se você não precisar do app em tempo real, pare-o para não incorrer em encargos inesperados.
{: tip}

## Próximas Etapas

* [Tutorials (Tutoriais)](/docs/tutorials/index.html)
* [Amostras ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
