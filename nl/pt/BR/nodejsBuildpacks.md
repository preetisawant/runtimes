---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Buildpacks Node.js

O {{site.data.keyword.Bluemix}} fornece várias versões do buildpack Node.js.
{: shortdesc}

* O buildpack **sdk-for-nodejs** do {{site.data.keyword.IBM_notm}} criado é o buildpack padrão
usado para aplicativos Node.js no {{site.data.keyword.Bluemix_notm}}.
* O **nodejs_buildpack** é um buildpack de comunidade fornecido pela comunidade do Cloud Foundry.

O buildpack **sdk-for-nodejs** tem precedência sobre o **nodejs_buildpack** em
{{site.data.keyword.Bluemix_notm}}. Se você deseja usar o **nodejs_buildpack** com o seu aplicativo em
vez do buildpack **sdk-for-nodejs**, deve-se especificar o seu buildpack, por exemplo, usando a opção `-b` com o comando `ibmcloud cf push`.

Geralmente, o buildpack **sdk-for-nodejs** atual e uma versão anterior estão disponíveis.  Para ver todos
os buildpacks disponíveis, use o comando `ibmcloud cf buildpacks`.  Por exemplo:

```
   ibmcloud cf buildpacks
   Getting buildpacks...

   buildpack                                 position   enabled   locked   filename   

   sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
   nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
   sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}
