---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-12"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Cloud Runtime for Swift
{: #swift_runtime}

O Runtime for Swift no {{site.data.keyword.Bluemix}} é desenvolvido com o builpack do [{{site.data.keyword.Bluemix_notm}} for Swift](https://github.com/IBM-Swift/swift-buildpack)
(isto é, swift_buildpack).
Esse buildpack fornece um ambiente de tempo de execução completo para aplicativos Swift.
{: shortdesc}

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix_notm}} fornece um [aplicativo iniciador ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Cloud/Kitura-Starter) do Swift baseado no Kitura. O app iniciador Kitura é um app Swift
simples que pode ser usado para saber mais sobre os tipos de aplicativos de servidor que
é possível desenvolver usando a linguagem de programação Swift. Esse app de amostra
cria um servidor HTTP Kitura básico que retorna conteúdo HTML para o cliente.

**Nota:** o aplicativo iniciador Kitura é destinado a ser usado para
propósitos educacionais. É possível experimentar com o aplicativo iniciador ao fazer aprimoramentos
e enviar essas mudanças por push para o ambiente do {{site.data.keyword.Bluemix_notm}}. Consulte [Usando os aplicativos iniciadores](../common/starter_app_usage.html) para obter ajuda sobre o uso
do aplicativo iniciador.

## Renomeando seu app
{: #renaming_your_app}

Se desejar renomear seu aplicativo, a partir do iniciador do Kitura ou em geral, haverá algumas
mudanças que precisarão ser feitas. Isso evitará confusão e assegurará uma
implementação sem erros.

- Renomeie a pasta do projeto do aplicativo para corresponder ao nome de seu app.
- `Package.swift` - Mude as entradas a seguir:
    - `name` - deve corresponder ao nome do app.
    - `targets[Target(name:)]` - deve corresponder ao nome do aplicativo
- `manifest.yml` - mude as entradas a seguir:
    - `name` - deve corresponder ao nome do app.
    - `Comando` - o nome do executável para iniciar seu aplicativo (deve corresponder ao
nome especificado no arquivo Package.swift).

## Versões de tempo de execução
{: #runtime_versions}

O [Runtime for Swift
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Swift/swift-buildpack)
(swift_buildpack) hospedado no {{site.data.keyword.Bluemix_notm}} é atualizado para usar a versão de GA mais recente dos
binários do Swift. Essa é a versão recomendada do Swift para uso no app. O buildpack lista outras versões do Swift em seu arquivo
[manifest.yml
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml),
que são armazenadas em cache no buildpack para conceder tempo de fornecimento reduzido.

Se você desejar usar uma versão diferente do Swift no {{site.data.keyword.Bluemix_notm}} para seu aplicativo, poderá especificar a versão com um arquivo `.swift-version` na raiz do repositório. Esse arquivo `.swift-version` define qual versão do Swift deve ser usada pelo swift_buildpack.

```
$ cat .swift-version
4.1.2
```
{: pre}

Como há atualizações frequentes de idioma do Swift, sempre será necessário incluir um arquivo `.swift-version` para que seu app seja "fixado" à versão do Swift com a
qual sabe-se que seu aplicativo funciona.

Observe que é possível especificar qualquer versão válida do Swift em seu arquivo
`.swift-version`. Essas versões alternativas devem corresponder à nomenclatura em
[Swift.org ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de linkexterno")](https://swift.org/download/), por meio do qual são diretamente transferidas por download. Embora o uso de uma versão

não em cache levará um pouco mais de tempo para provisionar, não há diferença de
desempenho de tempo de execução de seu app Swift.

O swift_buildpack padrão no {{site.data.keyword.Bluemix_notm}} será usado se o diretório-raiz
do seu aplicativo contiver um arquivo `Package.swift`.  Se
você desejar usar um buildpack alternativo, deverá especificar isso
incluindo uma entrada
`buildpack: {buildpackUrl}` no arquivo manifest.yml do seu app. Como alternativa, é possível definir isso no
momento da implementação, usando o argumento de comando `ibmcloud cf push -b {buildpackUrl}`.


## Ambientes do desenvolvedor

Os desenvolvedores têm diversas opções ao criar aplicativos do lado do servidor com
o Swift. Aqueles que usam um dispositivo Apple macOS podem preferir usar o IDE Xcode, embora isso não seja um requisito.  Apps baseados no Swift que serão implementados e
executados no {{site.data.keyword.Bluemix_notm}} podem usar qualquer editor de
programação ou IDE.  O destaque e a claridade da sintaxe para Swift estão disponíveis para
muitos editores populares. A ferramenta de linha de comandos REPL do Swift incluída nos binários de [Swift.org ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://swift.org/) permite compilação local e teste antes da implementação no {{site.data.keyword.Bluemix_notm}}.

Para os usuários do macOS, é possível usar o [app Kitura
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.kitura.io/app.html),
que simplifica a criação, a implementação, o gerenciamento e o controle dos apps Swift do lado do servidor que são executados no {{site.data.keyword.Bluemix_notm}}.  


## Integração aprimorada

O trabalho com a [estrutura da web Kitura](http://ibm-swift.github.io/Kitura/) fornece uma grande negociação de recursos. O Kitura é modular por natureza e você logo irá querer estender sua funcionalidade com SDKs empacotados, para fornecer recursos como autenticação, acesso a serviços baseados no Watson e uma ampla variedade de bancos de dados.  O Kitura fornece suporte para muitos bancos de dados diretamente, enquanto outros projetos de software livre também fornecem SDKs para muitas plataformas de banco de dados. A seguir está uma lista incompleta de SDKs fornecidos pela Kitura para trabalhar com recursos externos.

- [SDK do Swift do IBM Watson Developer Cloud
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/watson-developer-cloud/swift-sdk/)
- [SwiftMetrics ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/RuntimeTools/SwiftMetrics)
- [IBM Cloudant e CouchDB
![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Swift/Kitura-CouchDB)
- [KituraKit ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Swift/KituraKit)
- [Swift Kuery ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/Swift-Kuery/)
- [Swift Kuery ORM ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Swift/Swift-Kuery-ORM)

Para localizar mais pacotes do Swift a serem incluídos no aplicativo, acesse a seção Pacotes de [Kitura.io](https://www.kitura.io/packages.html). Os pacotes podem ser incluídos em um aplicativo Swift incluindo a URL do Git e os detalhes da versão do pacote no arquivo `Package.swift` do app. Para obter mais detalhes sobre gerenciamento de pacote, consulte a [seção Package Manager do Swift.org](https://swift.org/package-manager/).


## Informações relacionadas

Existem também outras ferramentas on-line disponíveis na IBM para o desenvolvedor do Swift.
- [IBM Swift DevCenter ![Ícone de link externo](../../icons/launch-glyph.svg "Íconede link externo")](https://developer.ibm.com/swift/) - Site de entrada principal para todas as informações

do IBM Swift. É possível encontrar informações sobre nossas ofertas, blogs, eventos sociais, documentação e muito mais.
- O [Kitura.io ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de linkexterno")](https://www.kitura.io/index.html) fornece notícias, amostras e recursos para a construção de aplicativos Kitura.

- O [Swift@IBM Slack ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://swift-at-ibm-slack.mybluemix.net/) fornece fóruns para fazer perguntas e resolver problemas com a equipe do Swift@IBM.
