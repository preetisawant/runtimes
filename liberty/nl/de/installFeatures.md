---

copyright:
  years: 2018
lastupdated: "2018-10-03"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# Liberty-Features installieren
{: #install-features}

Die Laufzeit von Liberty for Java umfasst eine [Untergruppe von Features](libertyFeatures.html#liberty_features), die in Liberty zur Verfügung stehen. Sie können Features installieren, die nicht in der Laufzeit enthalten sind; führen Sie hierfür den Liberty-Befehl `installUtility` als Cloud Foundry-Vor-Laufzeit-Hook aus, wenn die Anwendung per Push-Operation an die {{site.data.keyword.cloud_notm}} übertragen wird.

Eine vollständige Liste der verfügbaren Features finden Sie unter [Liberty-Features ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html).

Informationen zur Verwendung von Vor-Laufzeit-Hooks finden Sie in der Cloud Foundry-Dokumentation unter [Configure Pre-Runtime Hooks ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.cloudfoundry.org/devguide/deploy-apps/deploy-app.html#profile).

1. Erstellen Sie im Stammverzeichnis der Anwendung, die Sie über eine Push-Operation an {{site.data.keyword.cloud_notm}} übertragen möchten, ein Verzeichnis mit dem Namen `.profile.d`.

1. Erstellen Sie im Verzeichnis `.profile.d` eine Scriptdatei, die den Befehl `installUtility` ausführt, wie im folgenden Beispiel gezeigt.

   In diesem Beispiel wird das Feature `javaee-8.0` installiert.

   ```
   #!/bin/sh
   echo "Installing javaee-8.0"
   export PATH=$PATH:$HOME/.java/jre/bin

   $HOME/.liberty/bin/installUtility install javaee-8.0 --acceptLicense
   ```
   {: codeblock}

   Sie können mehrere Features installieren, indem Sie zusätzliche, durch Leerzeichen voneinander getrennte Namen von Features angeben.
   {: tip}

1. Übertragen Sie Ihre App per Push-Operation an die {{site.data.keyword.cloud_notm}}; verwenden Sie hierfür den Parameter `-p`, um das Stammverzeichnis der Anwendung anzugeben.

   Führen Sie z. B. den folgenden Befehl aus, um Ihre App per Push-Operation zu übertragen:
   ```
   ibmcloud cf push myApp -p /<path-to-application>
   ```
   {: codeblock}

1. Überprüfen Sie, ob das Feature erfolgreich installiert wurde, indem Sie das aktuelle Protokoll der Anwendung anzeigen.

   Führen Sie z. B. den folgenden Befehl aus, um das Protokoll anzuzeigen:
   ```
   ibmcloud cf logs myApp --recent
   ```
   {: codeblock}

    Wurde das Feature installiert, werden in der Ausgabe die folgenden Nachrichten angezeigt:

    ```
    2018-09-18T13:01:17.61-0400 [APP/PROC/WEB/0] OUT Installing javaee-8.0
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT Establishing a connection to the configured repositories ...
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT This process might take several minutes to complete.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Successfully connected to all configured repositories.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Preparing assets for installation. This process might take several minutes to complete.
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT The --acceptLicense argument was found. This indicates that you have
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT accepted the terms of the license agreement.
    ```
