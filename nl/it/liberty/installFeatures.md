---

copyright:
  years: 2018
lastupdated: "2018-12-14"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# Installa le funzioni Liberty
{: #install-features}

Il runtime Liberty for Java include [un sottoinsieme di funzioni](libertyFeatures.html#liberty_features) che sono disponibili in Liberty. Puoi installare le funzioni che non sono incluse nel runtime eseguendo il comando Liberty `installUtility` come un hook di pre-runtime di Cloud Foundry quando viene eseguito il push dell'applicazione a {{site.data.keyword.cloud_notm}}.

Per un elenco completo delle funzioni disponibili, vedi [Liberty features ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html).

Per informazioni sull'utilizzo degli hook di pre-runtime, vedi [Configure Pre-Runtime Hooks ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.cloudfoundry.org/devguide/deploy-apps/deploy-app.html#profile) nella documentazione di Cloud Foundry.

1. Nella directory root dell'applicazione di cui vuoi eseguire il push a {{site.data.keyword.cloud_notm}}, crea una directory `.profile.d`.

1. Nella directory `.profile.d`, crea un file script che esegue il comando `installUtility` come mostrato nel seguente esempio.

   Questo esempio installa la funzione `audit-1.0`.

   ```
   #!/bin/sh
   echo "Installing audit-1.0"
   export PATH=$PATH:$HOME/.java/jre/bin

   $HOME/.liberty/bin/installUtility install audit-1.0 --acceptLicense
   ```
   {: codeblock}

   Puoi installare più funzioni specificando dei nomi funzione aggiuntivi separati da spazi.
   {: tip}

1. Esegui il push della tua applicazione a {{site.data.keyword.cloud_notm}} utilizzando il parametro `-p` per specificare la directory root dell'applicazione.

   Ad esempio, esegui il seguente comando per eseguire il push della tua applicazione:
   ```
   ibmcloud cf push myApp -p /<path-to-application>
   ```
   {: codeblock}

1. Verifica che la funzione sia stata installata correttamente visualizzando il log recente dell'applicazione.

   Ad esempio, esegui il seguente comando per visualizzare il log.
   ```
   ibmcloud cf logs myApp --recent
   ```
   {: codeblock}

    Se la funzione è stata installata, l'output mostra i seguenti messaggi:

    ```
    2018-09-18T13:01:17.61-0400 [APP/PROC/WEB/0] OUT Installing audit-1.0
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT Establishing a connection to the configured repositories ...
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT This process might take several minutes to complete.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Successfully connected to all configured repositories.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Preparing assets for installation. This process might take several minutes to complete.
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT The --acceptLicense argument was found. This indicates that you have
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT accepted the terms of the license agreement.
    ```
