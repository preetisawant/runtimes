---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Paquetes de compilación Node.js

{{site.data.keyword.Bluemix}} proporciona varias versiones del paquete de compilación Node.js.
{: shortdesc}

* {{site.data.keyword.IBM_notm}} ha creado el paquete de compilación**sdk-for-nodejs** que es el paquete de compilación predeterminado que se utiliza para aplicaciones Node.js en {{site.data.keyword.Bluemix_notm}}.
* **nodejs_buildpack** es un paquete de compilación de comunidad proporcionado por la comunidad de Cloud Foundry.

El paquete de compilación **sdk-for-nodejs** tendrá precedencia sobre **nodejs_buildpack** en {{site.data.keyword.Bluemix_notm}}. Si desea utilizar **nodejs_buildpack** con la aplicación en lugar del paquete de compilación **sdk-for-nodejs**, debe especificar el paquete de compilación, por ejemplo, utilizando la opción `-b` con el mandato **cf push**.

Normalmente, están disponibles el paquete de compilación **sdk-for-nodejs** actual y una versión de nivel anterior.  Para ver todos los paquetes de compilación disponibles, utilice el mandato **cf buildpacks**.  Por ejemplo:

```
   cf buildpacks
   Getting buildpacks...

   buildpack                                 position   enabled   locked   filename   

   sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip
   nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip
   sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}
