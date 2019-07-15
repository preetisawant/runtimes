---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Pacchetti di build Node.js

{{site.data.keyword.Bluemix}} fornisce più versioni del pacchetto di build Node.js.
{: shortdesc}

* Il pacchetto di build **sdk-for-nodejs** creato da {{site.data.keyword.IBM_notm}} è il pacchetto di build predefinito utilizzato per le applicazioni Node.js in {{site.data.keyword.Bluemix_notm}}.
* Il **nodejs_buildpack** è il pacchetto di build esterno fornito dalla community Cloud Foundry.

Il pacchetto di build **sdk-for-nodejs** ha la precedenza su **nodejs_buildpack** in {{site.data.keyword.Bluemix_notm}}. Se vuoi
utilizzare **nodejs_buildpack** con la tua applicazione invece del pacchetto di build **sdk-for-nodejs**, devi
specificare il tuo pacchetto di build, ad esempio utilizzando l'opzione `-b` con il comando `ibmcloud cf push`.

Di norma, sono disponibili il pacchetto di build **sdk-for-nodejs** e una versione back-level.  Per visualizzare tutti i pacchetti di build disponibili, utilizza il comando `ibmcloud cf buildpacks`.  Ad esempio:

```
   ibmcloud cf buildpacks
   Getting buildpacks...

   buildpack                                 position   enabled   locked   filename   

   sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
   nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
   sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}
