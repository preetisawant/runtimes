---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilizar las características beta
{: #using_beta_features}

Las funciones beta de Liberty proporcionan un acceso previo a las nuevas funciones y modelos de programación que quizás se incluyan en un futuro release de Liberty. La mayoría de las funciones beta también se pueden utilizar en las aplicaciones desplegadas en {{site.data.keyword.Bluemix}}.

**Importante**: Las funciones beta están pensadas para entornos de desarrollo y prueba y no se deben utilizar en producción. Para ver las condiciones de uso completas, consulte el [ acuerdo de licencia beta ](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

Características beta de Liberty disponibles en {{site.data.keyword.Bluemix_notm}}
<table>
<tr>
<th align="left">Características</th>
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

Para poder utilizar las funciones beta de Liberty en {{site.data.keyword.Bluemix_notm}}, debe hacer lo siguiente:

1. [Desplegar un directorio del servidor o un servidor empaquetado](optionsForPushing.html) con una o varias funciones beta habilitadas en el archivo server.xml como en el ejemplo siguiente:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>mpOpenAPI-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Establezca la variable de entorno **IBM_LIBERTY_BETA** en **true**. Esta variable indica al paquete de compilación de Liberty que instale y habilite las funciones beta para la aplicación.  Por ejemplo:
  * utilizando la herramienta de línea de mandatos cf:
```
       $ cf set-env <nombre_app> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * o bien, utilizando el archivo manifest.yml:
```
      env:
          IBM_LIBERTY_BETA: "true"
```

3. Establezca la variable de entorno **JBP_CONFIG_LIBERTY** en **"version: +"**. Esta variable habilita el [tiempo de ejecución mensual de Liberty](buildpackDefaults.html#liberty_versions) que da soporte a funciones beta. Por ejemplo:
  * utilizando la herramienta de línea de mandatos cf:
```
       $ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * o bien, utilizando el archivo manifest.yml:
```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
```

Si está habilitando funciones beta en una aplicación existente, no olvide volver a transferir la aplicación después de establecer las variables de entorno.

{: #codeblock}

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Tiempo de ejecución de Liberty for Java](index.html)
* [Visión general de Liberty](https://www.ibm.com/support/knowledgecenter/SSAW57_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/cwlp_about.html)
