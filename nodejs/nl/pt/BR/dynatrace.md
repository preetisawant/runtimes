---

copyright:
  years: 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Use a Dynatrace para monitorar o Node.js no  {{site.data.keyword.cloud_notm}}
{: #using_dynatrace}

Dynatrace é um serviço de terceiro que fornece monitoramento para seu app. É possível integrar o Dynatrace com o seu aplicativo Node.js, mas a IBM não fornece suporte para serviços de terceiro. Consulte  [ Serviços de Terceiros ](../common/buildpackSupport.html#third-party)  para obter mais informações.

Para obter informações sobre o Dynatrace e suas licenças, consulte [Monitoramento de aplicativo Dynatrace![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.dynatrace.com/en/products/application-monitoring.html).

Quando o aplicativo Node.js está configurado para usar o Dynatrace, o tempo de execução do Node.js adquire uma plataforma
Dynatrace como um script de instalação de serviço (PaaS) de um site do Dynatrace e executa esse agente Dynatrace com o seu
aplicativo. Para integrar o Dynatrace ao seu aplicativo, é necessário criar um serviço fornecido pelo usuário e, em seguida, ligar o
serviço ao seu aplicativo.

## Integrando o Dynatrace com seu aplicativo

1. Efetue login em sua conta do Dynatrace e gere um token PaaS. Para obter detalhes, consulte a seção [Gerar token PaaS ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/how-do-i-monitor-cloud-foundry-applications/) na documentação de monitoramento do aplicativo do Cloud Foundry Dynatrace.

  Anote o seu ID do ambiente e o token.
1. Crie um serviço fornecido pelo usuário que aponte para suas credenciais do Dynatrace executando o comando a seguir. O nome
do serviço deve conter a sequência `dynatrace`, tal como `dynatrace-service`.

    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken"
    ```
    {: codeblock}
    
    **Nota:** não substitua `environmentid` ou `apitoken` pelas suas credenciais. Depois de executar o comando, você será solicitado a fornecer os seus valores.

    Se você estiver usando o Dynatrace Managed, inclua também o campo `apiurl`, que especifica o terminal de API de seu servidor gerenciado.
    
    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken, apiurl"
    ```
    {: codeblock}
    
    Quando solicitado depois de executar o comando, configure o `apiurl` como `https://<YourManagedServerURL>/e/<environmentID>/api `.
    
1. Após enviar por push o seu app para o {{site.data.keyword.Bluemix_notm}}, ligue o serviço fornecido pelo usuário que você criou ao app. Por exemplo, use o comando a seguir:
    ```
    ibmcloud cf bs myApp dynatrace-service
    ```
    {: codeblock}

    **Nota**: deve-se remontar o aplicativo após a ligação do serviço.

   Como alternativa, é possível ligar o serviço ao seu aplicativo incluindo o nome de seu serviço fornecido pelo usuário na
seção `service` do arquivo `manifest.yml` do seu aplicativo.
   ```yaml
   ---
    applications:
    - path: .
      memory: 256M
      instances: 1
      name: myApp
      host: myApp
      disk_quota: 1024M
    services:
      - dynatrace-service
   ```
   {: codeblock}
