---

copyright:
  years: 2016, 2017, 2018
lastupdated: "2018-01-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Trabalho no modo off-line para Node.js
{: #offline_mode}

Quando um aplicativo Node.js é enviado por push para {{site.data.keyword.Bluemix}}, o buildpack do SDK for Node.js
normalmente faz download de artefatos dos recursos externos, como os módulos de nó do NPM. Em algumas situações, como com [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) e
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), é possível customizar o acesso a sites externos ao {{site.data.keyword.Bluemix_notm}}.  
{: shortdesc}

O buildpack Node.js pode acessar os seguintes sites externos. Você pode precisar colocar esses sites em
uma *lista de desbloqueio* nos ambientes [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) e
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local)
{{site.data.keyword.Bluemix_notm}}.

* http://nodejs.org/ pode ser usado para determinar as versões do mecanismo de nó disponíveis.
* Https://s3pository.heroku.com é usado para recuperar as versões do mecanismo de nó não incluídas no buildpack.
*  https://www.npmjs.com/package/npm e https://semver.herokuapp.com são usados para recuperar as versões do npm não incluídas no buildpack.
* https://iojs.org é usado para recuperar a versão mais antiga do nó que não está contida no buildpack ou não está disponível em https://semver.herokuapp.com.
* https://registry.npmjs.org é usado para recuperar módulos de nó, como expresso.

Para minimizar o conjunto de sites incluídos na lista de desbloqueio, configure seus aplicativos para usar uma versão do
mecanismo de nó que está incluída no buildpack do SDK for Node.js. Consulte as [atualizações mais
recentes](./updates.html) para o conjunto de versões do mecanismo de nó incluídas no buildpack. Se você configurar seu aplicativo para usar
essas versões do mecanismo de nó, então apenas o site https://registry.npmjs.org será necessário para fazer download dos módulos.

Quando novas versões do buildpack do SDK for Node.js forem instaladas, o conjunto de versões disponíveis
do mecanismo frequentemente mudará para versões mais recentes. Talvez seja necessário reconfigurar seu aplicativo para especificar uma
versão de mecanismo do nó mais recente incluída no buildpack.


## Aplicativos off-line
{: #offline_applications}

Para eliminar a necessidade de acessar https://registry.npmjs.org, é possível incluir todos os módulos de nó que seu
aplicativo requer dentro de seu aplicativo. Para fazer isso, execute `npm install` para todos os módulos
aplicativos necessários e, em seguida, inclua o diretório *node_modules* resultante com seu aplicativo enviado por push.

Suas dependências podem ter dependências que possuam dependências e assim por diante, mas o `package.json`
conterá somente as dependências de nível superior. Se uma das dependências usar uma faixa no package.json e uma nova versão desta for liberada, os módulos no diretório node_modules poderão se tornar obsoletos. *Termo-retrátil* ajuda você a bloquear todas as versões de dependência para que isso não possa ocorrer.  
Para usar o termo-retrátil, comece com um diretório `node_modules` vazio ou limpo. Em seguida, no diretório-raiz do
seu projeto, execute:


1. ```npm install```
1. ```npm dedupe```
2. ```npm shrinkwrap```

Isso pode mudar o `package.json` e incluir o `npm-shrinkwrap.json` no diretório-raiz.
Sempre que você fizer uma mudança em dependências no arquivo `package.json`, repita as etapas `npm
dedupe` e `shringwrap`.

## Trabalhando com um proxy
{: #working_with_proxy}

Em alguns ambientes como
[{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) e
[{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local), um proxy pode ser configurado. Consulte
[Trabalhando com um proxy](/docs/manageapps/workingWithProxy.html) para obter mais detalhes.
