---

copyright: years: 2017 lastupdated: "2017-12-15"

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

Seguindo o tutorial de introdução do Tomcat, você irá configurar um ambiente de desenvolvimento, implementará um aplicativo
localmente e no {{site.data.keyword.Bluemix}} e integrará um serviço de banco de dados em seu aplicativo.

## Antes de Começar
{: #prereqs}

Você precisará do seguinte:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* [Maven ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat versão 8.0.41 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}


## Etapa 1: clonar o aplicativo de amostra
{: #clone}

Agora você está pronto para começar a trabalhar com o app Tomcat de amostra. Clone o repositório e mude para o diretório no qual o app de amostra está localizado.
```
git clone https://github.com/IBM-Bluemix/get-started-tomcat
```
{: pre}

```
cd get-started-tomcat
```
{: pre}

Examine os arquivos no diretório *get-started-tomcat* para familiarizar-se com o conteúdo.

## Etapa 2: executar o app localmente
{: #run_locally}

Deve-se instalar as dependências e construir um arquivo .war conforme definido no arquivo pom.xml para executar o app.

Instale as dependências.

```
mvn clean install  
```
{: pre}


Copie GetStartedTomcat.war do diretório `target` para o diretório `tomcat-install-dir` `webapps`.

Execute o app.  
```
<tomcat-install-dir>/bin/startup.bat|.sh
```
{: pre}

Visualize seu app em: http://localhost:8080/GetStartedTomcat/

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

Nesse arquivo manifest.yml, **random-route: true** gera uma rota aleatória para seu app para evitar que sua rota colida com outras.  Se você optar por isso, será possível substituir **random-route: true** por **host: myChosenHostName**, fornecendo um nome de host de sua preferência. [Saiba mais...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## Etapa 4: implementar o app
{: #deploy}

É possível usar a CLI do Cloud Foundry para implementar apps.

Escolha seu terminal de API

```
cf api <API-endpoint>
```
{:pre}

Substitua o *API-endpoint* no comando por um terminal de API da lista a seguir.

| **Nome da região** | **Local geográfico** | **Endpoint da API** |
|-----------------|-------------------------|-------------------|
| Região Sul dos EUA | Dallas, EUA | api.ng.bluemix.net |
| Região Leste dos EUA | Washington, DC, EUA | api.us-east.bluemix.net |
| Região do Reino Unido | Londres, Inglaterra | api.eu-gb.bluemix.net |
| Região de Sydney | Sydney, Austrália | api.au-syd.bluemix.net |
| Região da Alemanha | Frankfurt, Alemanha | api.eu-de.bluemix.net |
{: caption="Tabela 1.  {{site.data.keyword.cloud_notm}} lista de região" caption-side="top"}

Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}}:

```
cf login
```
{: pre}

Se não for possível efetuar login usando os comandos `cf login` ou `bx login` porque você tem um ID de usuário federado, use os comandos `cf login --sso` ou `bx login --sso` para efetuar login com seu ID de conexão única. Veja [Efetuando login com um ID federado](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id) para saber mais.

No diretório *get-started-tomcat*, envie seu app por push para o {{site.data.keyword.Bluemix_notm}}
```
cf push
```
{: pre}

Isso pode levar aproximadamente dois minutos. Se houver um erro no processo de implementação, será possível usar o comando `cf logs <Your-App-Name> --recent` para solucionar problemas.

Quando a implementação for concluída, você deverá ver uma mensagem indicando que o app está em execução.  Visualize o app na URL listada na saída do comando push.  Também é possível emitir o comando
  ```
cf apps
  ```
  {: pre}
  para visualizar o status dos apps e ver a URL.

## Etapa 5: incluir um banco de dados
{: #add_database}

Em seguida, vamos incluir um banco de dados NoSQL nesse aplicativo e configurar o aplicativo para que ele possa ser executado localmente e no {{site.data.keyword.Bluemix_notm}}.

1. Em seu navegador, efetue login no {{site.data.keyword.Bluemix_notm}} e acesse o Painel. Selecione seu aplicativo clicando em seu nome na coluna **Nome**.
2. Clique em **Conexões** e, em seguida, **Criar conexão**.
3. Na seção **Dados e Analytics**, selecione **Cloudant NoSQL DB** e, em seguida, crie o serviço.
4. Acesse **Aplicativos > Seu app > Conexões** e, em seguida, escolha **Conectar existente**.
5. Selecione **Remontar** quando solicitado. O {{site.data.keyword.Bluemix_notm}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_notm}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente que seja referenciada em seu código-fonte. [Saiba mais...](/docs/manageapps/depapps.html#app_env)
{: tip}

## Etapa 6: usar o banco de dados
{: #use_database}

Vamos agora atualizar seu código local para apontar para esse banco de dados. Vamos armazenar as credenciais dos serviços em um arquivo de propriedades. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente `VCAP_SERVICES`.

1. Em seu navegador, acesse {{site.data.keyword.Bluemix_notm}} e selecione **Apps > _seu app_ > Conexões > Cloudant > Visualizar credenciais**.

2. Copie e cole apenas a `URL` das credenciais no campo `URL` do arquivo `cloudant.properties` e salve as mudanças.
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:pre}

3. Reinicie o servidor

Atualize a visualização do navegador em: http://localhost:8080/GetStartedTomcat/. Os nomes que você inserir no app serão agora incluídos no banco de dados.

  Seu app local e o app {{site.data.keyword.Bluemix_notm}} estão compartilhando o banco de dados. Os nomes que você incluir de qualquer um dos apps aparecerão em ambos quando os navegadores forem atualizados.


Lembre-se, se você não precisar do app em tempo real no {{site.data.keyword.Bluemix_notm}}, pare-o para não incorrer em encargos inesperados.
{: tip}  

## Próximas Etapas

* [Tutorials (Tutoriais)](/docs/tutorials/index.html)
* [Amostras ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://ibm-cloud.github.io){: new_window}
* [Architecture Center ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
