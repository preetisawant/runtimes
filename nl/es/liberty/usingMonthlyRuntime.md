---

copyright:
  years: 2019
lastupdated: "2019-02-01"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilización del tiempo de ejecución mensual
{: #using_monthly_runtime}

El tiempo de ejecución mensual de Liberty proporciona la versión más reciente y acceso a nueva funcionalidad y modelos de programación.

Para utilizar el tiempo de ejecución mensual de Liberty en {{site.data.keyword.Bluemix_notm}}, deberá hacer lo siguiente:

Establezca la variable de entorno `JBP_CONFIG_LIBERTY` en `"version: +"` y la variable de entorno `IBM_LIBERTY_MONTHLY` en `true`. Estas variables habilitan el tiempo de ejecución mensual de [Liberty](/docs/runtimes/liberty/buildpackDefaults.html#liberty_versions). Por ejemplo:
  * Usando la herramienta de CLI de {{site.data.keyword.Bluemix_notm}}:
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_MONTHLY true
    ```
    {: .codeblock}

  * O, si utiliza el archivo `manifest.yml`:
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

Si está habilitando el tiempo de ejecución mensual en una aplicación existente, puede que necesite suprimir y volver a enviar por push la aplicación después de establecer las variables de entorno.
