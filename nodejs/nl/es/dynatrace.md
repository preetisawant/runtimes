---

copyright:
  years: 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilización de Dynatrace para supervisar Node.js en {{site.data.keyword.cloud_notm}}
{: #using_dynatrace}

Dynatrace es un servicio de otro proveedor que proporciona supervisión de la app. Puede integrar Dynatrace con la aplicación Node.js, pero IBM no proporciona soporte para servicios de terceros. Consulte [Servicios de terceros](../common/buildpackSupport.html#third-party) para obtener más información.

Para obtener información sobre Dynatrace y su licencia, consulte [Supervisión de la aplicación Dynatrace ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.dynatrace.com/en/products/application-monitoring.html).

Cuando la aplicación Node.js se configura para utilizar Dynatrace, el tiempo de ejecución de Node.js adquiere un script de instalación de plataforma como servicio (PaaS) de Dynatrace desde un sitio de Dynatrace y ejecuta dicho agente de Dynatrace con la app. Para integrar Dynatrace con la app, debe crear un servicio proporcionado por el usuario y, a continuación, enlazar el servicio a la app.

## Integración de Dynatrace con la aplicación

1. Inicie la sesión en la cuenta de Dynatrace y genere una señal PaaS. Para obtener detalles, consulte la sección [Generar señal de PaaS ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/how-do-i-monitor-cloud-foundry-applications/) en la documentación de supervisión de la app Dynatrace Cloud Foundry.

  Anote el ID de entorno y la señal.
1. Cree un servicio proporcionado por el usuario que apunte a sus credenciales de Dynatrace ejecutando el mandato siguiente. El nombre del servicio debe contener `dynatrace`, como por ejemplo, `dynatrace-service`.

    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken"
    ```
    {: codeblock}
    
    **Nota:** No sustituya `environmentid` ni `apitoken` por sus credenciales. Después de ejecutar el mandato, se le preguntará por sus valores.

    Si está utilizando Dynatrace Managed, añada también el campo `apiurl`, que especifica el punto final de la API del Servidor gestionado.
    
    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken, apiurl"
    ```
    {: codeblock}
    
    Cuando se le solicite después de ejecutar el mandato, establezca la `apiurl` en `https://<YourManagedServerURL>/e/<environmentID>/api`.
    
1. Una vez que haya enviado la app a {{site.data.keyword.Bluemix_notm}}, enlace el servicio proporcionado por el usuario que ha creado a la app. Por ejemplo, utilice el mandato siguiente:
    ```
    ibmcloud cf bs myApp dynatrace-service
    ```
    {: codeblock}

    **Nota**: Debe volver a transferir la aplicación después de enlazar el servicio.

   De forma alternativa, puede enlazar el servicio a la app añadiendo el nombre del servicio proporcionado por el usuario a la sección `service` del archivo `manifest.yml` de la app.
   ```yaml
   ---
    applications:
    - path: .
      memory: 256M
      instances: 1
      name: myApp
      host: myApp
      disk_quota: 1024M
    services:
      - dynatrace-service
   ```
   {: codeblock}
