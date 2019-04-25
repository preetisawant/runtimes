---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"
subcollection: "Nodejs"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Executar o aplicativo Node.js localmente
{: #hints}

Configure um número de porta para executar seu aplicativo Node.js localmente sem causar conflitos ao executá-lo em
{{site.data.keyword.Bluemix}}.
{: shortdesc}

Quando o aplicativo está em execução no {{site.data.keyword.Bluemix_notm}}, a variável de ambiente PORT é alocada pelo
Cloud Foundry. Porém, quando o aplicativo está executando localmente, PORT não é definido, assim, é possível definir a porta para
o seu aplicativo. Para evitar conflitos, defina para a porta na qual seu aplicativo atende localmente algo diferente da porta usada pelo {{site.data.keyword.Bluemix_notm}}.

No exemplo a seguir para um arquivo **js**, **3000** é usado como o número da
porta. Usando **3000**, é possível executar o aplicativo localmente para fins de teste e no
{{site.data.keyword.Bluemix_notm}} sem fazer mudanças.

```
var port = (process.env.PORT || 3000);
```
{: codeblock}
