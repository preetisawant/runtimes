---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Ruby
{: #ruby_runtime}

O tempo de execução Ruby no {{site.data.keyword.Bluemix}} foi desenvolvido com o ruby_buildpack.
O ruby_buildpack fornece um ambiente de tempo de execução completo para apps Ruby.
{: shortdesc}

O ruby_buildpack é usado se seu app possui um Gemfile no diretório-raiz. Neste caso, ele usará o Bundler para instalar suas dependências.

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix_notm}} fornece um app iniciador em Ruby.  O aplicativo iniciador em Ruby é um app em Ruby simples que fornece um modelo que pode
ser usado para seu app. É possível experimentar o app iniciador, fazendo e enviando mudanças por push para o ambiente
{{site.data.keyword.Bluemix_notm}}.  Consulte [Usando os aplicativos iniciadores](../common/starter_app_usage.html) para obter ajuda sobre o uso
do aplicativo iniciador.

## Versões de runtime
{: #runtime_versions}

É possível especificar a versão do Ruby a ser usada por seu aplicativo no Gemfile de seu aplicativo. Por exemplo:

```
  source 'https://rubygems.org'
  ruby '2.4.1'
  gem 'sinatra', '>= 0'
  gem 'haml', '>= 0'
  gem 'json', '>=0'
```
{: codeblock}

Quando uma versão não for especificada, a versão 2.4.1 será escolhida por padrão.

### Versões disponíveis:
{: #available_versions}

As seguintes versões do Ruby estão disponíveis no [buildpack do Ruby](https://github.com/cloudfoundry/ruby-buildpack/releases/tag/v1.6.34) atualmente instalado no {{site.data.keyword.Bluemix}}:

* 2.1.8
* 2.1.9
* 2.2.6
* 2.2.7
* 2.3.3
* 2.3.4
* 2.4.0
* 2.4.1

Se seu app requer uma versão do Ruby não listada, é possível usar o
[buildpack Ruby](https://github.com/cloudfoundry/ruby-buildpack) externo para implementar o app.

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Buildpack Cloud Foundry para Ruby](https://github.com/cloudfoundry/cf-buildpack-ruby)
* [Documentação do Ruby on Rails ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://api.rubyonrails.org/)
