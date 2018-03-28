---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Configurar serviços de limite
{: #auto_config}

É possível ligar vários serviços ao seu aplicativo Liberty for Java. Os serviços podem ser gerenciados por contêiner, por aplicativo ou por ambos, dependendo do que o desenvolvedor
deseja.

Um serviço gerenciado por aplicativo é um serviço que é inteiramente gerenciado pelo aplicativo,
sem qualquer assistência do Liberty. O aplicativo geralmente lê VCAP_SERVICES para obter informações sobre o serviço ligado
e acessa o serviço diretamente. O aplicativo fornece todo o código necessário de acesso ao cliente. Não há nenhuma dependência dos recursos do Liberty ou da configuração do arquivo server.xml. A configuração automática do buildpack
do Liberty não se aplica aos serviços deste tipo.

Um serviço gerenciado por contêiner é um serviço que é gerenciado pelo tempo de execução do Liberty. Em alguns casos, o aplicativo pode consultar o serviço ligado em JNDI, enquanto em outros o serviço é usado diretamente pelo próprio  Liberty. O buildpack do Liberty lerá VCAP_SERVICES para obter informações sobre os serviços ligados. Para cada serviço gerenciado por contêiner, o buildpack executa três funções.

* Gera [variáveis de nuvem](optionsForPushing.html#accessing_info_of_bound_services) para o serviço limite.
* Instala os recursos do Liberty e os códigos de acesso do cliente que são necessários para acessar o serviço de limite.
* Gera ou atualiza sub-rotinas do arquivo server.xml que são requeridas pelo serviço.

Este processo é referido como uma configuração automática.

O buildpack Liberty fornece configuração automática para os tipos de serviço a seguir:

* [Auto-Scaling](/docs/services/Auto-Scaling/index.html#autoscaling)
* [ClearDB MySQL Database ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.cleardb.com/developers)
* [Cloudant NoSQL Database](/docs/services/Cloudant/index.html#Cloudant)
* [Compose for MongoDB](/docs/services/ComposeForMongoDB/index.html)
* [Compose for MySQL](/docs/services/ComposeForMySQL/index.html)
* [Compose for PostgreSQL](/docs/services/ComposeForPostgreSQL/index.html)
* [dashDB](/docs/services/dashDB/index.html#dashDB)
* [ElephantSQL](docs/services/ElephantSQL/index.html)
* [Single Sign On](/docs/services/SingleSignOn/index.html#sso_gettingstarted)

Os serviços Compose podem ser gerenciados por contêiner ou gerenciados por aplicativo. Por padrão, o buildpack do Liberty
assume que esses serviços são gerenciados por contêiner e os configura automaticamente. Se desejar que o aplicativo gerencie o serviço,
você pode fazer opt-out da configuração automática para o serviço, configurando a variável
de ambiente `services_autoconfig_excludes`. Para obter mais informações, veja [Fazendo opt-out da configuração automática de serviço](autoConfig.html#opting_out).

## Instalação do código de acesso do cliente e dos recursos do Liberty
{: #installation_of_liberty_features}

Ao ligar a um serviço gerenciado por contêiner, o serviço pode requerer que os recursos do Liberty sejam configurados na sub-rotina featureManager no arquivo server.xml. O buildpack do  Liberty atualiza a sub-rotina featureManager e instala os binários de apoio necessários. Se o serviço precisar de jars do driver cliente, os jars serão transferidos por download para um local bem conhecido na instalação do Liberty.

Veja a seção [Fazendo opt-out da configuração automática de serviço](#opting_out) para obter mais detalhes sobre os tipos de serviço de limite.

## Gerando ou atualizando sub-rotinas de configuração do server.xml
{: #generating_or_updating_serverxml}

O buildpack do Liberty pode gerar ou atualizar automaticamente sub-rotinas de configuração em seu arquivo server.xml quando enviar
por push um aplicativo independente, dependendo de como seu aplicativo está ligado a serviços e se você tem um arquivo server.xml
existente.

Ao enviar por push um aplicativo independente, o buildpack do Liberty gera a sub-rotina de configuração server.xml, conforme
descrito em [Opções para enviar por push aplicativos do Liberty](optionsForPushing.html#options_for_pushing) para
{{site.data.keyword.Bluemix_notm}}.

Ao enviar por push um aplicativo independente e ligar aos serviços gerenciados por contêiner, o buildpack do Liberty gera as sub-rotinas necessárias do server.xml para os serviços ligados.

Ao fornecer um arquivo server.xml e ligar aos serviços gerenciados por contêiner, o buildpack do Liberty irá gerar ou
atualizar as sub-rotinas de configuração.

* Se o arquivo server.xml fornecido não contiver sub-rotinas de configuração para os serviços de limite, o Liberty gerará
a configuração para os serviços de limite.
* Se o arquivo server.xml fornecido contiver sub-rotinas de configuração para os serviços de limite, o Liberty atualizará a
configuração para esses serviços.

Consulte a documentação para o tipo de serviço ligado para obter
detalhes adicionais.

## Executando opt-out da configuração automática de serviço
{: #opting_out}

Em alguns casos, talvez você não queira que o buildpack do Liberty configure automaticamente os serviços que foram ligados. Considere os cenários a seguir:

* Meu aplicativo usa *dashDB*, mas desejo que o aplicativo gerencie diretamente a conexão com o banco de dados. O  aplicativo contém o jar do driver cliente necessário. 
Eu não desejo que o buildpack do Liberty configure automaticamente o serviço *dashDB*.
* Estou fornecendo um arquivo server.xml e forneci as sub-rotinas de configuração para a instância *cloudant*
porque preciso de uma configuração de origem de dados não padrão. Eu não desejo que o buildpack do Liberty atualize meu arquivo server.xml, mas ainda preciso que o buildpack do Liberty assegure que o software de apoio apropriado esteja instalado.

Para executar opt-out da configuração automática de serviço, use a variável de ambiente services_autoconfig_excludes. É possível incluir esta variável de ambiente em um manifest.yml ou configurá-la usando o cliente cf.

É possível executar opt-out da configuração automática de serviços em uma base por tipo de serviço. É possível escolher
fazer opt-out completamente (como no cenário *dashDB*) ou opt-out somente de atualizações de configuração do
arquivo server.xml (como no cenário *cloudant*). O valor que você especifica para a variável de ambiente
services_autoconfig_excludes é uma sequência conforme mostrado abaixo.

* A sequência pode conter especificações de opt-out para um ou mais serviços.
* A especificação de opt-out para um serviço específico é service_type=option, em que:
  * O service_type é o rótulo para o serviço conforme exibido em VCAP_SERVICES.
  * A opção é all ou config.
* Se a Sequência contiver uma especificação de opt-out para mais de um serviço, as especificações individuais de opt-out deverão ser separadas por um único caractere de espaço em branco.

Consulte o exemplo a seguir de gramática da sequência services_autoconfig_excludes:

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type (service label as it appears in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: codeblock}

**Importante**: O tipo de serviço que você especifica deve corresponder ao rótulo de serviços como ele aparece na variável de ambiente VCAP_SERVICES. O espaço em branco não é permitido.
**Importante**: Nenhum espaço em branco é permitido em um ```<service_type_specification>```. 
O único uso permitido de espaço em branco é separar múltiplas instâncias ```<service_type_specification>``` .

Use a opção **todos** para fazer opt-out de todas as ações de configuração automática para um
serviço, como no cenário *dashDB* acima. Use a opção **config** para fazer opt-out somente das
ações de atualização de configuração como no cenário *cloudant* acima.

Aqui estão especificações de opt-out de amostra em um arquivo manifest.yml para os cenários *dashDB* e
*cloudant*.

```
    env:
      services_autoconfig_excludes: dashDB=all

    env:
      services_autoconfig_excludes: cloudant=config

    env:
      services_autoconfig_excludes: cloudant=config dashDB=all
```
{: codeblock}

Aqui estão exemplos de como configurar a variável de ambiente services_autoconfig_excludes para o aplicativo myapp usando a interface de linha de comandos.

```
    cf set-env myapp services_autoconfig_excludes cloudant=config
    cf set-env myapp services_autoconfig_excludes "cloudant=config dashDB=all"
```
{: codeblock}

Para localizar o *label* para um serviço em VCAP_SERVICES, emita um comando como o exemplo a seguir:

```
    cf env myapp
```
{: codeblock}

A saída inclui texto semelhante ao seguinte, em que é possível ver o campo **label** com o valor **elephantsql**:

```
   "elephantsql": [
   {
      "credentials": {
      "max_conns": "5",
      "uri":      "..."
   },
   "label": "elephantsql",

```
{: codeblock}

## Substituindo a configuração de serviço
{: #override_service_config}

Em alguns casos, talvez você queira substituir a configuração padrão de um serviço gerado pela configuração automática.
É possível usar a variável de ambiente **LBP_SERVICE_CONFIG_xxxx** para substituir uma configuração de serviço. 
Consulte as tabelas a seguir para obter os nomes completos de variáveis de ambiente e a sintaxe de exemplo para substituí-las. Por
exemplo, para substituir a versão padrão do serviço *elephantSQL* e configurá-la para a versão 8.3.4.+,
emita um comando como:

```
    cf set-env myapp LBP_SERVICE_CONFIG_POSTGRESQL "{driver: { version: 8.3.4.+ }}"
```
{: codeblock}

Esta tabela mostra o mapeamento de **service_type** para nomes de variável de ambiente **LBP_SERVICE_CONFIG_xxxx**.

<table>
<tr>
<th align="left">service_type</th>
<th align="left">Nome da Variável de Ambiente</th>
</tr>

<tr>
<td>Auto-Scaling</td>
<td>LBP_SERVICE_CONFIG_AUTO-SCALING</td>
</tr>

<tr>
<td>cleardb</td>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
</tr>

<tr>
<td>cloudantNoSQLDB</td>
<td>LBP_SERVICE_CONFIG_CLOUDANTNOSQLDB</td>
</tr>

<tr>
<td>compose-for-mongodb</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MONGO</td>
</tr>

<tr>
<td>compose-for-mysql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
</tr>

<tr>
<td>compose-for-postgresql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
</tr>

<tr>
<td>elephantsql</td>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
</tr>

<tr>
<td>SingleSignOn</td>
<td>LBP_SERVICE_CONFIG_SINGLESIGNON</td>
</tr>
</table>


A tabela a seguir mostra a sintaxe para substituir algumas opções de configuração de serviço:

<table>
<tr>
<th align="left">Nome da Variável de Ambiente</th>
<th align="left">Sintaxe de configuração</th>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_MYSQL</td>
<td>"{driver: { version: x.y.z }, connection_pool_size: 15}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_COMPOSE_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_POSTGRESQL</td>
<td>"{driver: { version: x.y.z }}"</td>
</tr>
</table>



# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil Liberty](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
