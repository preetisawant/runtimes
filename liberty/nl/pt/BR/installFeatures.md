---

copyright:
  years: 2018
lastupdated: "2018-12-14"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# Instalar os recursos do Liberty
{: #install-features}

O tempo de execução do Liberty for Java inclui [um subconjunto de recursos](libertyFeatures.html#liberty_features) que estão disponíveis no Liberty. É possível instalar os recursos que não estão incluídos no tempo de execução executando o comando `installUtility` do Liberty como um gancho de pré-tempo de execução do Cloud Foundry quando o aplicativo é enviado por push para o {{site.data.keyword.cloud_notm}}.

Para obter uma lista completa dos recursos disponíveis, consulte [Recursos do Liberty ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html).

Para obter informações sobre como usar os ganchos de pré-tempo de execução, consulte [Configurar os ganchos de pré-tempo de execução![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.cloudfoundry.org/devguide/deploy-apps/deploy-app.html#profile) na documentação do Cloud Foundry.

1. No diretório-raiz do aplicativo que você deseja enviar por push para o {{site.data.keyword.cloud_notm}}, crie um diretório `.profile.d`.

1. No diretório `.profile.d`, crie um arquivo de script que executa o comando `installUtility` conforme mostrado no exemplo a seguir.

   Este exemplo instala o recurso  ` audit-1.0 ` .

   ```
   #!/bin/sh
   echo "Installing audit-1.0"
   export PATH=$PATH:$HOME/.java/jre/bin

   $HOME/ .liberty/bin/installUtility install audit-1.0 -- acceptLicense
   ```
   {: codeblock}

   É possível instalar múltiplos recursos especificando nomes de recursos adicionais separados por espaços.
   {: tip}

1. Envie por push o aplicativo para {{site.data.keyword.cloud_notm}} usando o parâmetro `-p` para especificar o diretório-raiz do aplicativo.

   Por exemplo, execute o comando a seguir para enviar por push o aplicativo:
   ```
   ibmcloud cf push myApp -p /<path-to-application>
   ```
   {: codeblock}

1. Verifique se o recurso foi instalado com êxito visualizando o log recente do aplicativo.

   Por exemplo, execute o comando a seguir para exibir o log:
   ```
   ibmcloud cf logs myApp --recent
   ```
   {: codeblock}

    Se o recurso foi instalado, a saída mostrará as mensagens a seguir:

    ```
    2018-09-18T13:01:17.61-0400 [APP/PROC/WEB/0] OUT Instalando o audit-1.0
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT Estabelecendo uma conexão com os repositórios configurados...
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT This process might take several minutes to complete.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Successfully connected to all configured repositories.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Preparing assets for installation. This process might take several minutes to complete.
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT The --acceptLicense argument was found. This indicates that you have
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT accepted the terms of the license agreement.
    ```
