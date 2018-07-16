---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-03"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Usar os recursos beta
{: #using_beta_features}

Os recursos beta do Liberty fornecem um acesso antecipado aos novos
modelos de programação e de funcionalidade que podem ser incluídos em uma liberação futura
do Liberty. A maioria dos recursos beta também podem ser usados em aplicativos
implementados no {{site.data.keyword.Bluemix}}.

**Importante**: os recursos beta são apenas para propósitos de desenvolvimento e de teste e não podem ser
usados em produção. Para obter os termos completos de uso, consulte o
[contrato de
licença beta](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

| Recursos |
| ------ |
| `appSecurity-3.0` |
| `audit-1.0` |
| `beanValidation-2.0` |
| `cdi-2.0` |
| `javaee-8.0` |
| `javaeeClient-8.0` |
| `jaxrs-2.1` |
| `jpa-2.2` |
| `jpaContainer-2.2` |
| `jsf-2.3` |
| `jsfContainer-2.3` |
| `jsonb-1.0` |
| `jsonbContainer-1.0` |
| `jsonp-1.1` |
| `jsonpContainer-1.1` |
| `logstashCollector-1.1` |
| `servlet-4.0` |
| `usageMetering-1.0` |
| `validator-1.0` |
| `webProfile-8.0` |
{: caption="Tabela 1. Recursos do Liberty Beta disponíveis no Liberty for Java em{{site.data.keyword.Bluemix_notm}}" caption-side="top"}


Para usar os recursos beta do Liberty no {{site.data.keyword.Bluemix_notm}}, será necessário fazer o seguinte:

1. [Implemente um diretório do servidor ou um servidor em pacote](optionsForPushing.html) com um ou mais recursos beta ativados no arquivo server.xml como no exemplo a seguir:

  ```
<server>
    <featureManager>
        <feature>servlet-4.0</feature>
        <feature>webProfile-8.0</feature>
    </featureManager>
</server>
  ```
  {: .codeblock}

2.  Configure a variável de ambiente `IBM_LIBERTY_BETA` como `true`. Essa variável direciona o buildpack do Liberty para instalar
e ativar os recursos beta em seu aplicativo.  Por exemplo:
  * Usando o [ {{site.data.keyword.Bluemix_notm}}  CLI (../ ../cli/reference/bluemix_cli/download_cli.html):
    ```
    ibmcloud cf set-env < yourappname> IBM_LIBERTY_BETA true
    ```
    {: .codeblock}

  * Ou, usando o arquivo `manifest.yml`:
    ```
      env:
          IBM_LIBERTY_BETA: "true"
    ```
    {: .codeblock}

3. Configure a variável de ambiente `JBP_CONFIG_LIBERTY` como
`"version: +"`. Essa variável ativa o [Tempo de execução mensal do Liberty ](buildpackDefaults.html#liberty_versions), que suporta os recursos beta. Por exemplo:
  * Usando a ferramenta CLI do  {{site.data.keyword.Bluemix_notm}} :
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ```
    {: .codeblock}

  * Ou, usando o arquivo `manifest.yml`:
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
    ```
    {: .codeblock}

Se você estiver ativando os recursos beta em um aplicativo existente, não se esqueça de remontar o seu aplicativo depois de configurar as variáveis de ambiente.
