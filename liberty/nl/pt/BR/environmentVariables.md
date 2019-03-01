---

copyright:
  years: 2015, 2019
lastupdated: "2018-02-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Variáveis de ambiente
{: #environment_variables}

Variáveis de ambiente suportadas pelo Liberty for Java.

<table>
<tr>
<th align="left">Nome da Variável de Ambiente</th>
<th align="left">Descrição</th>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_ENABLE</td>
<td>Ative os [utilitários de gerenciamento de app](/docs/runtimes-common/app_mng.html)</td>
</tr>

<tr>
<td>BLUEMIX_APP_MGMT_INSTALL</td>
<td>Instale os [utilitários de gerenciamento de app](/docs/runtimes-common/app_mng.html)</td>
</tr>

<tr>
<td>IBM_LIBERTY_MONTHLY</td>
<td>Ativar  [ Tempo de execução de liberação mensal do Liberty / ](/docs/runtimes/liberty/usingMonthlyRuntime.html)</td>
</tr>

<tr>
<td>JAVA_OPTS</td>
<td>Configure as [opções Java](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_DYNATRACEAPPMONAGENT</td>
<td>Configure as [informações de local do agente Dynatrace](/docs/runtimes/liberty/monitoring/dynatrace.html#configuring_liberty_app)</td>
</tr>

<tr>
<td>JBP_CONFIG_IBMJDK </td>
<td>Configure a [versão do IBM JRE](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_LIBERTY</td>
<td>Configure uma variedade de opções de tempo de execução do Liberty incluindo [recursos para arquivos WAR ou EAR](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)</td>
</tr>

<tr>
<td>JBP_CONFIG_OPENJDK</td>
<td>Configure a [versão do OpenJDK](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JBP_CONFIG_SPRINGAUTORECONFIGURATION </td>
<td>Desative a
[Estrutura
de reconfiguração automática Spring](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/framework-spring_auto_reconfiguration.md). Para desativar, configure o valor para ativado: falso. </td>
</tr>

<tr>
<td>JBP_LOG_LEVEL</td>
<td>Configure o nível de criação de log do buildpack. Valores possíveis: <b>DEBUG</b>, <b>INFO</b> (padrão), <b>WARN</b>, <b>ERROR</b> ou <b>FATAL</b></td>
</tr>

<tr>
<td>JVM</td>
<td>Selecione o [tipo de JRE](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>JVM_ARGS</td>
<td>Configure os [argumentos da JVM](/docs/runtimes/liberty/customizingJRE.html)</td>
</tr>

<tr>
<td>LBP_SERVICE_CONFIG_xxxx</td>
<td>[Substituir a configuração de serviço](/docs/runtimes/liberty/autoConfig.html#override_service_config)</td>
</tr>

<tr>
<td>HTTP_PROXY</td>
<td>Configure informações do servidor proxy</td>
</tr>

<tr>
<td>HTTPS_PROXY</td>
<td>Configure informações do servidor proxy</td>
</tr>

<tr>
<td>services_autoconfig_excludes</td>
<td>Desative a [configuração automática](/docs/runtimes/liberty/autoConfig.html#opting_out) do serviço.</td>
</tr>
</table>
{: caption="Tabela 1. Variáveis de ambiente disponíveis para o Liberty for Java" caption-side="top"}

## Atributos desativados no buildpack do Liberty for Java

Há alguns atributos que são automaticamente desativados pelo buildpack do Liberty, que não podem ser substituídos. As
variáveis de ambiente e os atributos a seguir são desativados.

### Tabela de atributos desativada

<table>
<tr>
<th>Atributo desativado </th>
<th>Elemento</th>
</tr>

<tr>
<td>host</td>
<td>httpEndpoint</td>
</tr>

<tr>
<td>httpPort</td>
<td>httpEndpoint</td>
</tr>

<tr>
<td>trustHostHeaderPort</td>
<td>webContainer</td>
</tr>

<tr>
<td>andextractHostHeaderPort</td>
<td>webContainer</td>
</tr>

<tr>
<td>logDirectory</td>
<td>criação de log</td>
</tr>

<tr>
<td>consoleLogLevel</td>
<td>criação de log</td>
</tr>

<tr>
<td>enableWelcomePage</td>
<td>httpDispatcher</td>
</tr>
</table>
{: caption="Tabela 1. Atributos desativados pelo Liberty for Java" caption-side="top"}
