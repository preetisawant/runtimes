---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-03"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilizar las características beta
{: #using_beta_features}

Las funciones beta de Liberty proporcionan un acceso previo a las nuevas funciones y modelos de programación que quizás se incluyan en un futuro release de Liberty. La mayoría de las funciones beta también se pueden utilizar en las aplicaciones desplegadas en {{site.data.keyword.Bluemix}}.

**Importante**: Las funciones beta están pensadas para entornos de desarrollo y prueba y no se pueden utilizar en producción. Para ver las condiciones de uso completas, consulte el [ acuerdo de licencia beta](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

| Características |
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
{: caption="Tabla 1. Características Beta de Liberty disponibles en Liberty for Java en {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

Para utilizar las funciones beta de Liberty en {{site.data.keyword.Bluemix_notm}}, deberá hacer lo siguiente:

1. [Desplegar un directorio del servidor o un servidor empaquetado](optionsForPushing.html) con una o varias funciones beta habilitadas en el archivo server.xml como en el ejemplo siguiente:

  ```
<server>
    <featureManager>
        <feature>servlet-4.0</feature>
        <feature>webProfile-8.0</feature>
    </featureManager>
</server>
  ```
  {: .codeblock}

2.  Establezca la variable de entorno `IBM_LIBERTY_BETA` en `true`. Esta variable indica al paquete de compilación de Liberty que instale y habilite las funciones beta para la aplicación.  Por ejemplo:
  * Usando la [CLI de {{site.data.keyword.Bluemix_notm}} (../../cli/reference/bluemix_cli/download_cli.html):
    ```
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_BETA true
    ```
    {: .codeblock}

  * O, si utiliza el archivo `manifest.yml`:
    ```
      env:
          IBM_LIBERTY_BETA: "true"
    ```
    {: .codeblock}

3. Establezca la variable de entorno `JBP_CONFIG_LIBERTY` en `"version: +"`. Esta variable habilita el [tiempo de ejecución mensual de Liberty](buildpackDefaults.html#liberty_versions) que da soporte a funciones beta. Por ejemplo:
  * Usando la herramienta de CLI de {{site.data.keyword.Bluemix_notm}}:
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ```
    {: .codeblock}

  * O, si utiliza el archivo `manifest.yml`:
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
    ```
    {: .codeblock}

Si está habilitando funciones beta en una aplicación existente, no olvide volver a transferir la aplicación después de establecer las variables de entorno.
