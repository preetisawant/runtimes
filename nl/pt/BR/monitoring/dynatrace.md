---

copyright:
  years: 2016, 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Use Dynatrace para monitorar o Liberty no {{site.data.keyword.cloud_notm}}
{: #using_dynatrace}

Dynatrace é um serviço de terceiro que fornece monitoramento para seu app. É possível integrar o Dynatrace com o seu aplicativo Liberty, mas a IBM não fornece suporte para serviços de terceiro. Consulte  [ Serviços de Terceiros ](../../common/buildpackSupport.html#third-party)  para obter mais informações.

Para obter mais informações sobre o Dynatrace e o seu licenciamento, consulte [Monitoramento de aplicativo Dynatrace![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](http://www.dynatrace.com/en/products/application-monitoring.html).

Quando o seu aplicativo Liberty é configurado para usar o Dynatrace, o comportamento padrão é que o tempo de execução do Liberty obtenha um arquivo `.jar` do agente Dynatrace de um site do Dynatrace e execute esse agente Dynatrace com o seu aplicativo.  Com esse
comportamento padrão, a configuração mínima necessária para usar o Dynatrace é criar um
serviço fornecido pelo usuário que aponte para o coletor Dynatrace.

## Criando um serviço fornecido pelo usuário que aponta para o coletor Dynatrace

Em primeiro lugar, você precisará configurar um coletor Dynatrace.  Em seguida,
deve-se criar um serviço fornecido pelo usuário para passar as informações do agente
Dynatrace para conexão com o coletor Dynatrace. Consulte [Arquitetura do Dynatrace![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo") ](https://community.dynatrace.com/community/display/DOCDT65/Architecture) para entender melhor o relacionamento entre os componentes Dynatrace.

1. Configure um coletor Dynatrace.
  * Consulte o [website da comunidade Dynatrace ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace) para obter instruções sobre como fazer download e configurar o coletor Dynatrace.
  * Assegure-se de que o coletor esteja configurado em um local que seja acessível ao agente Dynatrace em execução com seu aplicativo no {{site.data.keyword.Bluemix_notm}}.
2. Crie um serviço fornecido pelo usuário que aponte para o coletor Dynatrace em execução.

  ** Nota:** o nome do serviço fornecido pelo usuário deve conter a sequência **dynatrace**. Letras maiúsculas e minúsculas são ignoradas. Por exemplo, use o comando a seguir, em que **my-dynatrace-collector** contém **dynatrace**:
  ```
  ibmcloud cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
  ```
  {: codeblock}

    Neste exemplo, my-dynatrace-collector é o nome fornecido ao serviço, DynatraceCollectorIPaddress é o endereço IP do coletor Dynatrace configurado por você e profile é o nome do perfil Dynatrace opcional associado a esse app monitorado. O valor do perfil padrão é Monitoring. É possível especificar parâmetros opcionais, como no exemplo que segue.

    ```
    ibmcloud cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                      "options" : {"dynatrace-parameter-1": "value",
                                   "dynatrace-parameter-2": "value"}}'
    ```
    {: codeblock}

    Veja a seção [_Configurações do agente_ de Configuração do agente ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://community.dynatrace.com/community/display/DOCDT65/Set+up+Agents) no website de comunidade do Dynatrace, para obter mais informações sobre as opções disponíveis. Por exemplo, usando a opção exclude, é possível excluir classes de serem monitoradas pelo Dynatrace. Consulte [Estrutura do agente Dynatrace ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md) para obter mais detalhes sobre como configurar o serviço fornecido pelo usuário.

3. Após enviar por push o seu app para o {{site.data.keyword.Bluemix_notm}}, ligue o serviço fornecido pelo usuário que você criou ao app. Por exemplo, use o comando a seguir:
  ```
  ibmcloud cf bs myApp my-dynatrace-collector
  ```
  {: codeblock}

    **Nota:** deve-se remontar o aplicativo após a ligação do serviço.

## Configuração opcional
{: #optional_configuration}

Você pode optar por adquirir e hospedar você mesmo o arquivo `.jar` do agente Dynatrace.  Nesse caso, são necessárias as etapas adicionais de configuração a seguir.
1. Adquira e hospede o arquivo `.jar` do agente Dynatrace para que o buildpack do Liberty possa fazer o seu download.
2. Configure seu app Liberty para que ele possa fazer download do agente Dynatrace.

### Hospedando o agente Dynatrace
{: #hosting_dynatrace_agent}
O agente Dynatrace deve ser hospedado em um servidor da web e o buildpack do Liberty deve ser capaz de fazer download do arquivo `.jar` do agente desse servidor. O servidor deve ser configurado com um arquivo `index.yml` que especifique detalhes sobre o arquivo `.jar` do agente. Conclua as etapas a seguir para configurar o agente Dynatrace:
  1. Faça download do arquivo  ` .jar `  do agente Dynatrace. Consulte [Instaladores da plataforma do servidor do Dynatrace ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace) no website da comunidade do Dynatrace para obter instruções sobre como fazer download do arquivo `.jar` do agente Dynatrace. O arquivo `.jar` do agente apropriado para execução no {{site.data.keyword.Bluemix_notm}} é a versão **6.+** do **dynatrace-agent-unix.jar**.
  2. Hospede o arquivo `.jar` do agente em um local do qual o buildpack do Liberty possa fazer seu download. É possível hospedá-lo no {{site.data.keyword.Bluemix_notm}} usando as instalações do servidor disponível ou é possível hospedá-lo em alguns locais disponíveis publicamente.
     * Assegure-se de fornecer um arquivo `index.yml` no local de hosting. O arquivo `index.yml` deve conter uma entrada que consista no ID da versão do arquivo `.jar` do agente seguido por dois pontos e a URL completa do local do arquivo `.jar` desse agente. Por exemplo:

            ---
               6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
            {: codeblock}

     * O arquivo **dynatrace-agent-6.3.0-unix.jar** deve estar disponível no local especificado no arquivo `index.yml`. O local para o arquivo `.jar` e o `index.yml` pode ser o mesmo diretório.

### Configurando o app Liberty
{: #configuring_liberty_app}

O aplicativo Liberty que você deseja monitorar deve ser configurado para localizar o servidor que está hospedando o arquivo `.jar` do agente que você configurou anteriormente. É possível configurar o app com a variável de ambiente **JBP_CONFIG_DYNATRACEAPPMONAGENT**. A variável de ambiente **JBP_CONFIG_DYNATRACEAPPMONAGENT** informa ao buildpack de onde fazer download do agente Dynatrace. Para configurar a variável de ambiente, conclua estas etapas:

1. Configure a variável **JBP_CONFIG_DYNATRACEAPPMONAGENT** para que tenha o valor *"repository_root: URL_of_server_hosting_index.yml"*. Por exemplo, depois de enviar por push seu aplicativo, emita o comando a seguir:

        ibmcloud cf se myApp JBP_CONFIG_DYNATRACEAPPMONAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
        {: codeblock}

    Neste exemplo, *my-dynatrace-agent-host.mybluemix.net* é a URL do arquivo `index.yml` hospedado pelo servidor configurado anteriormente.

2. Depois de configurar a variável de ambiente, remonte seu app. Verifique se no log de preparação há uma mensagem indicando o download bem-sucedido do agente Dynatrace no servidor hosting do agente. Por exemplo:
```
    Fazendo download do dynatrace-agent-6.3.0-unix.jar 6.3.0 a partir de https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
```
{: codeblock}
