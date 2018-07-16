---

copyright:
  years: 2017, 2018
lastupdated: "2018-04-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Gravar aplicativos da web Java seguros
{: #secure_java_web_app}

Todos os aplicativos da web devem ser projetados e codificados visando segurança para evitar a introdução de vulnerabilidades severas de segurança.
{: shortdesc}

O {{site.data.keyword.Bluemix}} fornece um aplicativo iniciador seguro para ajudar a escrever código Java Liberty mais seguro e evitar a maioria dos problemas Cross-Site Scripting (XSS). É possível fazer download deste [aplicativo iniciador seguro](https://github.com/IBM-Cloud/java-secure-app), construí-lo e implementá-lo localmente e no {{site.data.keyword.Bluemix_notm}}.

## Por que escrever apps da web seguros
{: #why}

Uma vulnerabilidade de segurança pode ser explorada por vários ataques de segurança. Um ataque pode roubar credenciais, causar perda de dados e função, interromper serviços, além de danificar a reputação e a renda de um negócio. O Cross-Site Scripting, XSS, é uma das vulnerabilidades de segurança comuns encontradas na maioria dos aplicativos da web que devem ser evitadas.

Em vez de aprender a teoria sobre ataques XSS e as técnicas reparatórias antes de iniciar o desenvolvimento de aplicativos da web, é possível usar este [aplicativo iniciador seguro](https://github.com/IBM-Cloud/java-secure-app). O aplicativo iniciador seguro inclui exemplos de codificação de práticas de codificação seguras essenciais que evitam o XSS para que você possa iniciar o desenvolvimento enquanto aprende e aplica técnicas de prevenção do XSS.

## Como usar o app de amostra seguro
{: #how}

É possível usar o [aplicativo iniciador seguro](https://github.com/IBM-Cloud/java-secure-app) como um ponto de início para o novo desenvolvimento de aplicativo Liberty. Comece aprendendo o código de contramedida XSS no app e, em seguida, aplique-o às operações da API do aplicativo. As contramedidas no aplicativo iniciador seguro ajudam a evitar que a entrada maliciosa do usuário danifique seu aplicativo tanto no servidor quanto no navegador, minimizando ou evitando ataques XSS.

Primeiramente, faça download desse aplicativo iniciador seguro e, em seguida, construa-o e implemente-o no
{{site.data.keyword.Bluemix_notm}} ou localmente da mesma maneira que você faz com o aplicativo de amostra [getting-started-java](https://github.com/IBM-Cloud/get-started-java).  Acesse [Introdução ao Liberty no {{site.data.keyword.Bluemix_notm}}](getting-started.html) para saber mais
sobre a construção e a implementação de aplicativos no {{site.data.keyword.Bluemix_notm}}.  Para iniciar, é possível usar essas etapas para clonar, construir e executar o app.

```
git clone https://github.com/IBM-Cloud/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
Visualize o app em http://localhost:9080/GetStartedSecureJava/

## Impingir HTTPS em todas as páginas em seu aplicativo
{: #enforce_https}

Para impingir HTTPS em vez de HTTP em todas as páginas em seu aplicativo, as mudanças a seguir precisam ser feitas.

Modifique o server.xml para ativar o recurso `appSecurity-2.0`:

```
  <featureManager>
    <feature>appSecurity-2.0</feature>
  </featureManager>
```

Modifique o arquivo web.xml para incluir a restrição de segurança a seguir:

```
  <security-constraint>
    <web-resource-collection>
      <web-resource-name>Entire Application</web-resource-name>
      <url-pattern>/*</url-pattern>
    </web-resource-collection>
    <user-data-constraint>
      <transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
  </security-constraint>
```

Isso faz seu aplicativo forçar todas as conexões para usar HTTPS automaticamente e não permitirá quaisquer conexões HTTP.

## Mais informações
{: more}
O aplicativo iniciador seguro contém **BadServlet.java**. Esse aplicativo mostra um exemplo de código inseguro que os desenvolvedores poderão escrever se não tomarem cuidado.

O aplicativo iniciador seguro também contém **GoodServlet.java**, que inclui várias boas práticas de codificação segura, como validação de entrada, codificação de saída, configurações de cabeçalho de HTTP seguras, além de Política de segurança de conteúdo. Essas práticas são contramedidas importantes contra XSS. Aplicá-las também pode minimizar outras vulnerabilidades, como alguma injeção e passagem de diretório.

Consulte [Folha de dicas de prevenção de XSS ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.owasp.org/index.php/XSS){: new_window} para saber mais sobre XSS e suas contramedidas.
