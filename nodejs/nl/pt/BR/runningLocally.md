---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Executar o aplicativo Node.js localmente
{: #hints}

Use estas informações para facilitar a execução do seu aplicativo Node.js localmente e no {{site.data.keyword.Bluemix}}.
{: shortdesc}

O exemplo a seguir mostra parte da origem para um arquivo **js**:
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

Com este código, quando o aplicativo está em execução no Bluemix, a variável de ambiente PORT contém o valor de porta que é interno para o Bluemix e no qual o app atende as conexões recebidas. Quando o
aplicativo está sendo executado localmente, PORT não está definido, de modo que **3000** é
usado como o número da porta. Gravando dessa maneira, é possível executar o aplicativo localmente para fins de teste e no Bluemix sem fazer mudanças adicionais.
