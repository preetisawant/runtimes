---

copyright:
  years: 2019
lastupdated: "2019-02-01"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Usar o tempo de execução mensal
{: #using_monthly_runtime}

O tempo de execução mensal do Liberty fornece a versão mais recente e o acesso a novos modelos de funcionalidade e de programação.

Para usar os recursos do Liberty mensalmente no {{site.data.keyword.Bluemix_notm}}, será necessário fazer o seguinte:

Configure a variável de ambiente `JBP_CONFIG_LIBERTY` como a variável de ambiente `"version: +"` e `IBM_LIBERTY_MONTHLY` como `true`. Essas variáveis ativam o [tempo de execução mensal do Liberty](/docs/runtimes/liberty/buildpackDefaults.html#liberty_versions). Por exemplo:
  * Usando a ferramenta CLI do  {{site.data.keyword.Bluemix_notm}} :
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ibmcloud cf set-env < yourappname> IBM_LIBERTY_MONTHLY true
    ```
    {: .codeblock}

  * Ou, usando o arquivo `manifest.yml`:
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
          IBM_LIBERTY_MONTHLY: true
    ```

    ```
      env:
          JBP_CONFIG_LIBERTY: "[version: +, app_archive: {features: [javaee-8.0]}]"
          IBM_LIBERTY_MONTHLY: true
    ```
    {: .codeblock}

Se ativar o tempo de execução mensal em um aplicativo existente, poderá ser necessário excluir e enviar seu aplicativo por push novamente depois de configurar as variáveis de ambiente.
