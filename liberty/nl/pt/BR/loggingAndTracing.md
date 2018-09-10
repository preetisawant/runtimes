---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Configure a criação de log e o rastreio
{: #logging_tracing}

## Arquivos de log
{: #log_files}

Os logs padrão do Liberty, tais como `messages.log` ou o diretório `ffdc`, estão disponíveis no {{site.data.keyword.Bluemix}} no diretório `logs` de cada instância do aplicativo. Esses logs podem ser acessados do console do {{site.data.keyword.Bluemix_notm}} ou por meio da CLI do {{site.data.keyword.Bluemix_notm}}. Por exemplo:

* Para acessar os logs recentes de um app, execute o comando a seguir:

  ```
  ibmcloud cf logs --recent <appname>
  ```
  {: codeblock}


* Para ver o arquivo `messages.log` de um aplicativo, execute o comando a seguir:

  ```
  ibmcloud cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

O nível de log e outras opções de rastreio podem ser configurados por meio do arquivo de configuração do Liberty. Para obter mais informações, consulte [Resolução de problemas do Liberty: criação de log e rastreio](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html).

## Usando os recursos de rastreio e de dump
{: #using_trace_and_dump}

### Usando rastreio e dump no console do {{site.data.keyword.Bluemix_notm}} (descontinuado)

A configuração de rastreio do Liberty pode ser ajustada para um aplicativo em execução diretamente do console do {{site.data.keyword.Bluemix_notm}}. O console também fornece capacidade para solicitar e fazer download de dumps de encadeamento e de heap. Para ajustar a configuração de rastreio ou solicitar um dump, selecione um aplicativo Liberty no console do {{site.data.keyword.Bluemix_notm}} e escolha o menu `Runtime` na navegação. Na visualização `Tempo de execução`, selecione uma instância e pressione o botão *RASTREIO* ou *DUMP*. Se estiver ajustando o nível de rastreio, consulte [Resolução de problemas do Liberty: criação de log e rastreio](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html) para os detalhes da sintaxe da especificação de rastreio.

### Mudando a configuração de rastreio por meio de SSH

Ao enviar o aplicativo por push, o arquivo server.xml inclui as propriedades padrão
**updateTrigger** configuradas para **pesquisadas** e **monitorInterval** configurado como 1 minuto. O
servidor Liberty é automaticamente configurado para verificar se há atualizações para o arquivo server.xml a cada minuto.

Consulte [Enviar
por push os apps Liberty com o server.xml](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing) para ver as opções de envio por push dos apps Liberty com um arquivo
`server.xml` customizado.

Consulte
[Controlando
as atualizações dinâmicas](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window} para ver como configurar a atualização dinâmica no arquivo server.xml.

Siga estas etapas para mudar a configuração de rastreio:

1. SSH para o seu app

  ```
 ibmcloud cf ssh < appname> [-i instance_index ]
  ```
  {: codeblock}

2. Editar  `<logging traceSpecification="xxxx"/>` no server.xml para configurar a sua especificação de
rastreio desejada, por exemplo, usando *vi*:

  ```
vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: codeblock}

Nota: a mudança do server.xml será perdida em uma remontagem ou reinicialização e será válida somente para a instância na qual você usar ssh.

Consulte [Resolução de problemas do Liberty: criação de log e rastreio](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window} para os detalhes da sintaxe da especificação de rastreio.

### Acionamento de dumps via SSH

Use o comando abaixo para acionar um encadeamento e um dump do heap por meio da CLI do
{{site.data.keyword.Bluemix_notm}} usando o recurso SSH:

  ```
 ibmcloud cf ssh <appname> -c "pkill -3 java"
  ```
  {: codeblock}

Veja a documentação abaixo para obter detalhes sobre o download dos arquivos de dump gerados.

## Fazer download de arquivos de dump
{: #download_dumps}

Por padrão, os vários arquivos de dump são colocados no diretório `dumps` do contêiner de aplicativo. Use o
`ibmcloud cf ssh` da CLI do {{site.data.keyword.Bluemix_notm}} para visualizar e fazer download dos arquivos dump.

* Para ver os dumps gerados, execute o comando a seguir:

  ```
  ibmcloud cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Para fazer download de um arquivo de dump, execute o comando a seguir:

  ```
  ibmcloud cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

Também é possível usar `scp` e outras ferramentas semelhantes para visualizar e fazer download dos arquivos de dump. Consulte [Acessando apps com SSH ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) para obter mais informações.

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Tempo de execução do Liberty](index.html)
* [Visão geral do Liberty](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
