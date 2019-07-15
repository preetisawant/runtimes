---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Usar o comando de inicialização
{: #startup_commmand}

As maneiras recomendadas para especificar um comando inicial para seu aplicativo {{site.data.keyword.Bluemix}} Node.js são usar um arquivo **Procfile** ou **package.json**.
{: shortdesc}

1. Especifique um comando de startup em seu **Procfile** da forma a seguir. Neste caso, _app.js_ é o script js de inicialização para seu aplicativo.
```
web: node app.js
```
{: codeblock}

1. Salve o
**Procfile** no diretório-raiz de seu aplicativo.

Se um **Procfile** não estiver presente, o buildpack {{site.data.keyword.Bluemix_notm}} Node.js
verificará uma entrada scripts.start no arquivo **package.json**. Novamente,
no exemplo abaixo, app.js é o script js de inicialização para seu aplicativo.
```
{
    ...   
    "scripts": {
      "início": "node app.js"
    }
}
```
{: codeblock}

Se uma entrada do script de início estiver presente no **package.json**, um
**Procfile** será automaticamente gerado. O conteúdo do **Procfile** gerado automaticamente é:
```
    web: npm start
```
{: codeblock}

Para obter mais informações sobre o arquivo **Procfile** e **package.json**, veja [Dicas para aplicativos Node.js ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).
