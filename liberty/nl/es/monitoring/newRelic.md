---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-12"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilice New Relic para supervisar Liberty en {{site.data.keyword.cloud_notm}}
{: #new_relic}

New Relic es un servicio de otro proveedor que proporciona métricas de supervisión de la aplicación. Para obtener más información sobre lo que ofrece el servicio New Relic, consulte [New
Relic](http://newrelic.com/java).

Según la [documentación sobre instalación manual del agente Java](https://docs.newrelic.com/docs/agents/java-agent/installation/java-agent-manual-installation), las aplicaciones Java que vaya a supervisar el servicio New Relic deben estar empaquetadas y configuradas con un agente New Relic y una clave de licencia de la cuenta. En el entorno de {{site.data.keyword.Bluemix}}, se puede obtener una cuenta y un acuerdo de licencia de New Relic creando una instancia de servicio en {{site.data.keyword.Bluemix_notm}}. Las aplicaciones Java se pueden enlazar a la instancia
de servicio de New Relic y el paquete de compilación de Liberty configura la de forma automática la aplicación que está lista para que la supervise el servicio
New Relic.
En concreto, el paquete de compilación:

* proporciona a la aplicación un agente New Relic.
* obtiene el nombre de la aplicación y la clave de licencia de las variables de entorno de la aplicación VCAP_APPLICATION y VCAP_SERVICES.
* configura las propiedades y la plantilla de configuración que necesita el agente New Relic.

Consulte la configuración de ejemplo que genera el paquete de compilación de
Liberty para la aplicación:

```
    -javaagent:/home/vcap/app/.new_relic_agent/new_relic_agent-3.12.0.jar
    -Dnewrelic.home=/home/vcap/app/.new_relic_agent
    -Dnewrelic.config.license_key=123456
    -Dnewrelic.config.app_name=myapp
    -Dnewrelic.config.log_file_path=../../../../../logs
```
{: codeblock}


## Añada un servicio New Relic proporcionado por el usuario
{: #add_user_provided_new_relic} 

Si ya dispone de una clave de licencia y de una cuenta de New Relic, debe enlazar el servicio
New Relic existente a la aplicación mediante un "servicio proporcionado por el usuario".

1. Cree una instancia de servicio proporcionada por el usuario utilización su clave de licencia existente.  Por ejemplo, si su clave de licencia existente es 1234567, puede utilizar la CLI de {{site.data.keyword.Bluemix_notm}} para crear el servicio proporcionado por el usuario ("create-user-provided-service") y proporcionar la clave de licencia 1234567 en el indicador como se muestra a continuación:

  ```
    ibmcloud cf create-user-provided-service mynewrelic -p "licenseKey"
    licenseKey> 1234567
  ```
  {: codeblock}

2. Despliegue la aplicación en {{site.data.keyword.Bluemix_notm}} con la instancia de servicio New Relic proporcionada por el usuario.  A continuación encontrará un manifiesto de ejemplo que utiliza una instancia de servicio New Relic proporcionada por el usuario:
  <pre>
        &dash;&dash;&dash;
        applications:
        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
         - mynewrelic
  </pre>
  {: codeblock}

3. Acceda al panel de control de New Relic para ver las métricas de aplicaciones.

La configuración automática del servicio New Relic es distinta de la configuración automática de otros servicios, ya que es un servicio gestionado por contenedor que está disponible a través de la infraestructura del paquete de compilación.  Puesto que está disponible a través de la infraestructura, la configuración automática de este servicio difiere de la de otros servicios en tres puntos:
* La exclusión no se ofrece como opción.
* La integración del servicio se basa en el agente New Relic, un agente Java. Por lo tanto, se configura mediante opciones de Java, no mediante variables de nube en el archivo server.xml.
* La configuración se basa tanto en VCAP_SERVICES como en VCAP_APPLICATION.
