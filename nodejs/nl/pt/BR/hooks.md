---

copyright:
  years: 2018
lastupdated: "2018-11-09"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# Integre serviços de terceiro usando ganchos
{: #hooks}

É possível usar ganchos para integrar facilmente os serviços de terceiro no buildpack do SDK for Node.js. Observe que a IBM não fornece suporte para nenhum serviço de terceiro que você integrar. Para obter mais informações sobre o suporte, consulte [Serviços de terceiro](/docs/runtimes-common/buildpackSupport.html#third-party).

O buildpack do SDK for Node.js inclui o gancho Dynatrace. O Dynatrace permite o monitoramento de aplicativos Node.js. Saiba mais sobre como usar o gancho Dynatrace no buildpack na [Documentação do Dynatrace ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")]( https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/application-only/deploy-oneagent-on-cloud-foundry-for-application-only-monitoring/){: new_window}.


Ao seguir as instruções na documentação de terceiro, lembre-se de usar o comando `ibmcloud cf` em vez do `cf` para executar os comandos para o buildpack do {{site.data.keyword.Bluemix_notm}}.
{: tip}
