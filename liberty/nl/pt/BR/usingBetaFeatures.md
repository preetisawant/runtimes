---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Usar os recursos beta
{: #using_beta_features}

Os recursos beta do Liberty fornecem um acesso antecipado aos novos
modelos de programação e de funcionalidade que podem ser incluídos em uma liberação futura
do Liberty. A maioria dos recursos beta também podem ser usados em aplicativos
implementados no {{site.data.keyword.Bluemix}}.

**Importante**: os recursos beta são somente para propósitos de teste e desenvolvimento e não podem ser usados em produção. Para obter os termos de
uso completos, consulte o [
contrato de licença beta](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

Recursos beta do Liberty disponíveis no {{site.data.keyword.Bluemix_notm}}
<table>
<tr>
<th align="left">Recursos</th>
</tr>

<tr>
    <tr><td>appSecurity-3.0</tr></td>
    <tr><td>audit-1.0</tr></td>
    <tr><td>beanValidation-2.0</tr></td>
    <tr><td>bluemixLogCollector-1.1</tr></td>
    <tr><td>cdi-2.0</tr></td>
    <tr><td>javaee-8.0</tr></td>
    <tr><td>javaeeClient-8.0</tr></td>
    <tr><td>jaxrs-2.1</tr></td>
    <tr><td>jpa-2.2</tr></td>
    <tr><td>jpaContainer-2.2</tr></td>
    <tr><td>jsf-2.3</tr></td>
    <tr><td>jsfContainer-2.2</tr></td>
    <tr><td>jsonb-1.0</tr></td>
    <tr><td>jsonbContainer-1.0</tr></td>
    <tr><td>jsonp-1.1</tr></td>
    <tr><td>jsonpContainer-1.1</tr></td>
    <tr><td>logstashCollector-1.1</tr></td>
    <tr><td>mpConfig-1.2</tr></td>
    <tr><td>mpOpenAPI-1.0</tr></td>
    <tr><td>mpRestClient-1.0</tr></td>
    <tr><td>opentracing-1.0</tr></td>
    <tr><td>servlet-4.0</tr></td>
    <tr><td>validator-1.0</tr></td>
    <tr><td>webProfile-8.0</tr></td>

</tr>
</table>

Para usar os recursos beta do Liberty no {{site.data.keyword.Bluemix_notm}} você precisará fazer o seguinte:

1. [Implemente um diretório do servidor ou um servidor em pacote](optionsForPushing.html) com um ou mais recursos beta ativados no arquivo server.xml como no exemplo a seguir:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>mpOpenAPI-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Configure a variável de ambiente **IBM_LIBERTY_BETA** como **true**. Essa variável direciona o buildpack do Liberty para instalar
e ativar os recursos beta em seu aplicativo.  Por exemplo:
  * usando a ferramenta de linha de comandos cf:
```
       $ cf set-env <yourappname> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * ou usando o arquivo manifest.yml:
```
      env:
          IBM_LIBERTY_BETA: "true"
```

3. Configure a variável de ambiente **JBP_CONFIG_LIBERTY** como
**"version: +"**. Essa variável ativa o [tempo de execução mensal do Liberty](buildpackDefaults.html#liberty_versions) que suporta recursos beta. Por exemplo:
  * usando a ferramenta de linha de comandos cf:
```
       $ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * ou usando o arquivo manifest.yml:
```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
```

Se você estiver ativando os recursos beta em um aplicativo existente, não se esqueça de remontar seu aplicativo após a configuração das variáveis de ambiente.

{: #codeblock}

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Tempo de execução do Liberty for Java](index.html)
* [Visão geral do Liberty](https://www.ibm.com/support/knowledgecenter/SSAW57_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/cwlp_about.html)
