---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}

O tempo de execução PHP no {{site.data.keyword.Bluemix}} foi desenvolvido com o php_buildpack.
O php_buildpack fornece um ambiente de tempo de execução completo para apps em PHP.
{: shortdesc}

O php_buildpack é usado nas condições a seguir:
* Seu app contém um arquivo composer.json ou
* seu app contém um arquivo *.php, ou
* seu app define uma variável ${WEBDIR} em seu arquivo
[options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html) e essa variável está configurada para
um diretório existente dentro de seu app.

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix}} fornece um app iniciador em PHP.  O aplicativo iniciador em PHP é um app em PHP simples que fornece um modelo
que pode ser usado para seu app. É possível experimentar o app iniciador, fazendo e enviando mudanças por push para o ambiente
{{site.data.keyword.Bluemix}}.  Consulte [Usando os aplicativos iniciadores](/docs/cfapps/starter_app_usage.html) para
obter ajuda sobre o uso do app iniciador.

## Impingir HTTPS em todas as páginas em seu aplicativo
{: #enforce_https}

Para impor o uso de HTTPS em vez de HTTP em todas as páginas em seu aplicativo ao executar no
{{site.data.keyword.Bluemix_notm}} usando o Apache, as mudanças a seguir precisam ser feitas ao seu arquivo ".htaccess".  Essa regra se aplicará a qualquer solicitação que não tiver sido feita usando somente HTTPS enquanto estiver executando no {{site.data.keyword.Bluemix_notm}}.

```
RewriteCond %{HTTP:X-Forwarded-Proto} !=https [NC]
RewriteCond %{ENV:BLUEMIX_REGION} !^$
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

## Versões de tempo de execução
{: #runtime_versions}

É possível especificar a versão do PHP a ser usado por seu app no arquivo composer.json. Por exemplo:

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
Para obter mais informações, veja [Links do pacote do Composer ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://getcomposer.org/doc/04-schema.md#package-links).

Quando uma versão não for especificada, a versão 5.6.31 será escolhida por padrão.

### Versões disponíveis:
{: #available_versions}

As seguintes versões do PHP estão disponíveis no [buildback
PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.27) atualmente instalado no {{site.data.keyword.Bluemix}}:

* 5.6.30
* 5.6.31
* 7.0.20
* 7.0.21
* 7.1.6
* 7.1.7

Se seu app requer uma versão do PHP não listada, é possível usar o [buildpack
PHP](https://github.com/cloudfoundry/php-buildpack.git) externo para implementar o app.

# rellinks
{: #rellinks notoc}
## Tutoriais e amostras
{: #samples notoc}
* [Compilar e implementar uma API REST](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Compilar e implementar um contador de calorias fácil de usar em dispositivos móveis ](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## geral
{: #general notoc}
* [Buildpack do Cloud Foundry para PHP](https://github.com/cloudfoundry/php-buildpack.git)
