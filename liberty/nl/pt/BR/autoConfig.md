---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Configurar serviços de limite
{: #auto_config}

É possível ligar vários serviços ao seu aplicativo Liberty for Java. Os serviços podem ser gerenciados por contêiner, por aplicativo ou por ambos, dependendo do que o desenvolvedor
deseja.

Um serviço gerenciado por aplicativo é um serviço inteiramente gerenciado pelo aplicativo, sem qualquer assistência do Liberty. O aplicativo geralmente lê VCAP_SERVICES para obter informações sobre o serviço ligado
e acessa o serviço diretamente. O aplicativo fornece todo o código necessário de acesso ao cliente. Não há dependência dos recursos do Liberty ou da configuração do arquivo `server.xml`. A configuração automática do buildpack
do Liberty não se aplica aos serviços deste tipo.

Um serviço gerenciado por contêiner é um serviço gerenciado pelo tempo de execução do Liberty. Em alguns casos, o aplicativo pode consultar o serviço ligado em JNDI, enquanto em outros o serviço é usado diretamente pelo próprio  Liberty. O buildpack do Liberty lerá VCAP_SERVICES para obter informações sobre os serviços ligados. Para cada serviço gerenciado por contêiner, o buildpack executa três funções.

* Gera [variáveis de nuvem](/docs/runtimes/liberty/optionsForPushing.html#accessing_info_of_bound_services) para o serviço limite.
* Instala os recursos do Liberty e os códigos de acesso do cliente que são necessários para acessar o serviço de limite.
* Gera ou atualiza sub-rotinas do arquivo `server.xml`
que são necessárias pelo serviço.

Este processo é referido como uma configuração automática.

O buildpack Liberty fornece configuração automática para os tipos de serviço a seguir:

* [{{site.data.keyword.autoscaling}}](/docs/services/Auto-Scaling/index.html#autoscaling)
* [ClearDB MySQL Database ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.cleardb.com/developers)
* [{{site.data.keyword.cloudant}}](/docs/services/Cloudant/index.html#Cloudant)
* [{{site.data.keyword.composeForMongoDB}}](/docs/services/ComposeForMongoDB/index.html)
* [{{site.data.keyword.composeForMySQL}}](/docs/services/ComposeForMySQL/index.html)
* [{{site.data.keyword.composeForPostgreSQL}}](/docs/services/ComposeForPostgreSQL/index.html)
* [{{site.data.keyword.dashdbshort}}](/docs/services/dashDB/index.html#dashDB)
* [ElephantSQL](/docs/services/ElephantSQL/index.html)
* [{{site.data.keyword.ssoshort}}](/docs/services/SingleSignOn/index.html#sso_gettingstarted)

Os serviços Compose podem ser gerenciados por contêiner ou gerenciados por aplicativo. Por padrão, o buildpack do Liberty
assume que esses serviços são gerenciados por contêiner e os configura automaticamente. Se desejar que o aplicativo gerencie o serviço,
você pode fazer opt-out da configuração automática para o serviço, configurando a variável
de ambiente `services_autoconfig_excludes`. Para obter mais informações, veja [Fazendo opt-out da configuração automática de serviço](/docs/runtimes/liberty/autoConfig.html#opting_out).

## Instalação do código de acesso do cliente e dos recursos do Liberty
{: #installation_of_liberty_features}

Ao se ligar a um serviço gerenciado por contêiner, o serviço pode requerer que os recursos do Liberty sejam configurados na sub-rotina `featureManager` no arquivo `server.xml`. O buildpack do Liberty atualiza a sub-rotina `featureManager` e instala os arquivos binários de apoio necessários. Se o serviço requerer arquivos JAR do driver do cliente, eles serão transferidos por download para uma localização bem conhecida na instalação do Liberty.

Consulte a seção [Fazendo opt-out da configuração automática de serviço](#opting_out) para obter mais
detalhes sobre os tipos de serviço de limite.

## Gerando ou atualizando sub-rotinas de configuração do server.xml
{: #generating_or_updating_serverxml}

O buildpack do Liberty pode gerar ou atualizar automaticamente as sub-rotinas de configuração no arquivo `server.xml` quando um aplicativo independente é enviado por push, dependendo de como o aplicativo está ligado aos serviços e se há um arquivo `server.xml` existente.

Ao enviar por push um aplicativo independente, o buildpack do Liberty gera a sub-rotina de configuração `server.xml`, conforme descrito em [Opções para enviar por push os aplicativos do Liberty](/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing), para o {{site.data.keyword.Bluemix_notm}}.

Ao enviar por push um aplicativo independente e ligar aos serviços gerenciados por contêiner, o buildpack do Liberty gera as sub-rotinas `server.xml` necessárias para os serviços ligados.

Quando um arquivo `server.xml` for fornecido e ligado aos serviços gerenciados por contêiner, o buildpack do Liberty gerará ou atualizará as sub-rotinas de configuração.

* Se o arquivo `server.xml` fornecido não contiver as sub-rotinas de configuração para os serviços ligados, o Liberty gerará a configuração para eles.
* Se o arquivo `server.xml` fornecido contiver as sub-rotinas de configuração para os serviços ligados, o Liberty atualizará a configuração para eles.

Consulte a documentação para o tipo de serviço ligado para obter
detalhes adicionais.

## Executando opt-out da configuração automática de serviço
{: #opting_out}

Em alguns casos, talvez você não queira que o buildpack do Liberty configure automaticamente os serviços que foram ligados. Considere os cenários a seguir:

* Meu aplicativo usa *dashDB*, mas desejo que o aplicativo gerencie diretamente a conexão com o banco de dados. O aplicativo contém o arquivo JAR do driver do cliente necessário. Eu não desejo que o buildpack do Liberty configure automaticamente o serviço *dashDB*.
* Estou fornecendo um arquivo `server.xml` e forneci as sub-rotinas de configuração para a instância *cloudant* porque preciso de uma configuração de origem de dados não padrão. Não desejo que o buildpack do Liberty atualize meu arquivo
`server.xml`, mas ainda preciso que o buildpack do Liberty assegure que o software de apoio apropriado
esteja instalado.

Para executar opt-out da configuração automática de serviço, use a variável de ambiente services_autoconfig_excludes. É
possível incluir essa variável de ambiente em um manifest.yml ou configurá-lo usando o cliente {{site.data.keyword.Bluemix_notm}}.

É possível executar opt-out da configuração automática de serviços em uma base por tipo de serviço. É possível escolher fazer opt-out completamente (como no cenário *dashDB*) ou fazer opt-out somente das atualizações de configuração do arquivo `server.xml` (como no cenário *cloudant*). O valor que você especifica para a variável de ambiente
services_autoconfig_excludes é uma sequência conforme mostrado abaixo.

* A sequência pode conter especificações de opt-out para um ou mais serviços.
* A especificação de opt-out para um serviço específico é service_type=option, em que:
  * O service_type é o rótulo para o serviço conforme exibido em VCAP_SERVICES.
  * A opção é `all` ou `config`.
* Se a sequência contiver uma especificação de opt-out para mais de um serviço, as especificações de opt-out individuais deverão ser separadas por um único caractere de espaço em branco.

Consulte o exemplo a seguir da gramática da sequência `services_autoconfig_excludes`:

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type (service label as it appears in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: codeblock}

**Importante**: O tipo de serviço que você especifica deve corresponder ao rótulo de serviços como ele aparece na variável de ambiente VCAP_SERVICES. O espaço em branco não é permitido.
**Importante**: nenhum espaço em branco é permitido em um `<service_type_specification>`. O
único uso permitido de espaço em branco é para separar múltiplos `<service_type_specification>`  instâncias.

Use a opção **todos** para fazer opt-out de todas as ações de configuração automática para um
serviço, como no cenário *dashDB* acima. Use a opção **config** para fazer opt-out somente das
ações de atualização de configuração como no cenário *cloudant* acima.

Aqui estão as especificações de opt-out de amostra em um arquivo `manifest.yml` para os cenários *dashDB* e *cloudant*.

```
    env:
      services_autoconfig_excludes: dashDB=all

    env:
      services_autoconfig_excludes: cloudant=config

    env:
      services_autoconfig_excludes: cloudant=config dashDB=all
```
{: codeblock}

Aqui estão os exemplos de como configurar a variável de ambiente `services_autoconfig_excludes` para o aplicativo `myapp` usando a interface da linha de comandos.

```
    ibmcloud cf set-env myapp services_autoconfig_excludes cloudant=config
    ibmcloud cf set-env myapp services_autoconfig_excludes "cloudant=config dashDB=all"
```
{: codeblock}

Para localizar o *label* para um serviço em VCAP_SERVICES, emita um comando como o exemplo a seguir:

```
    ibmcloud cf env myapp
```
{: codeblock}

A saída inclui texto semelhante ao seguinte, em que é possível ver o campo `label` com o valor **elephantsql**:

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
É possível usar a variável de ambiente **LBP_SERVICE_CONFIG_xxxx** para substituir uma configuração de serviço. Consulte as tabelas a seguir para obter os nomes completos de variáveis de ambiente e a sintaxe de exemplo para substituí-las.  Por
exemplo, para substituir a versão padrão do serviço *elephantSQL* e configurá-la para a versão 8.3.4.+,
emita um comando como:

```
    ibmcloud cf set-env myapp LBP_SERVICE_CONFIG_POSTGRESQL "{driver: { version: 8.3.4.+ }}"
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
<td>LBP_SERVICE_CONFIG_POSTGRESQL</td>
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
