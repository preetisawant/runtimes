---

copyright:
  years: 2018
lastupdated: "2018-11-09"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# Integrar servicios de terceros mediante hooks
{: #hooks}

Puede utilizar hooks para integrar fácilmente servicios de terceros en el paquete de compilación SDK for Node.js. Tenga en cuenta que IBM no proporciona soporte para ningún servicio de terceros que integre. Para obtener más información sobre el soporte, consulte [Servicios de terceros](../common/buildpackSupport.html#third-party).

El paquete de compilación SDK for Node.js incluye el hook Dynatrace. Dynatrace permite la supervisión de aplicaciones Node.js. Obtenga más información sobre cómo utilizar el hook Dynatrace en el paquete de compilación en la [documentación de Dynatrace ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")]( https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/application-only/deploy-oneagent-on-cloud-foundry-for-application-only-monitoring/){: new_window}.


Cuando siga las instrucciones de la documentación de terceros, recuerde utilizar el mandato `ibmcloud cf` en lugar de `cf` para ejecutar mandatos para el paquete de compilación de {{site.data.keyword.Bluemix_notm}}.
{: tip}
