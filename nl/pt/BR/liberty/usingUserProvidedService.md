---

copyright:
  years: 2017, 2018
lastupdated: "2018-6-26"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Usando um serviço fornecido pelo usuário com o Liberty no {{site.data.keyword.cloud_notm}}
{: #using_user_provided}

O Cloud Foundry fornece um mecanismo para se conectar e usar serviços que
não são necessariamente fornecidos ou disponibilizados em seu ambiente do {{site.data.keyword.Bluemix_notm}}.
Esse recurso é  [ Serviços Fornecidos pelo Usuário ](https://docs.cloudfoundry.org/devguide/services/user-provided.html).

Este documento pressupõe que:
  * você tem algum serviço disponível,
  * é possível obter credenciais para esse serviço
e descreve as etapas necessárias para se conectar e usar esse serviço com o
aplicativo de amostra Getting-Started-Liberty

Para essa discussão, usaremos a instância do CloudantNoSQLDB como nosso serviço de exemplo
e será criado um serviço fornecido pelo usuário para se conectar a ele.

## Etapa 1: Push do aplicativo Getting-Started
{: #follow_getting_started}

Siga as etapas no [Tutorial de introdução](/docs/runtimes/liberty/getting-started.html) enviando
o aplicativo por push para o {{site.data.keyword.Bluemix_notm}}.  Pare antes de conectar o banco de dados.

## Etapa 2: criar uma instância do CloudantNoSQLDB
{: #create_cloudantnosqldb}

Siga as etapas no [Tutorial de introdução](/docs/runtimes/liberty/getting-started.html)
para criar uma instância do CloudantNoSqLDB

Use a opção de visualização de credenciais para copiar as credenciais do CloudandNoSQLDB. Salve essas credenciais em um arquivo local, por exemplo, cloudant-creds.

## Etapa 3: Criar um serviço fornecido pelo usuário
Para trabalhar com o aplicativo Getting-Started,
o nome do serviço fornecido pelo usuário deve conter
"cloudantNoSQLDB".  O aplicativo Getting-Started está analisando
a variável de serviços VCAP e procurando um serviço fornecido pelo usuário
com um nome que contém "cloudantNoSQLDB".

        ibmcloud cf cups my-cloudantNoSQLDB-ups -p cloudant-creds

## Etapa 4: ligar o serviço fornecido pelo usuário e remontar o app
Ligue o serviço fornecido pelo usuário ao aplicativo Getting-Started.

        ibmcloud cf bs GettingStartedLiberty my-cloudantNoSQLDB-ups

        ibmcloud cf restage GettingStartedLiberty

## Etapa 5: Confirmar
Navegue até o aplicativo e confirme se é possível
incluir vários nomes no campo 'name'.
