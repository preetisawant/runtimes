---

copyright:
  years: 2019
lastupdated: "2019-02-01"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Monatliche Laufzeit verwenden
{: #using_monthly_runtime}

Mit der monatlichen Liberty-Laufzeit stehen die neueste Version sowie Zugriff auf neue Funktionen und Programmiermodelle zur Verfügung. 

Gehen Sie wie folgt vor, um die monatliche Liberty-Laufzeit in {{site.data.keyword.Bluemix_notm}} zu verwenden: 

Legen Sie für die Umgebungsvariable `JBP_CONFIG_LIBERTY` den Wert `"version: +"` und für die Umgebungsvariable `IBM_LIBERTY_MONTHLY` den Wert `true` fest. Mit diesen Variablen wird die [monatliche Liberty-Laufzeit](/docs/runtimes/liberty/buildpackDefaults.html#liberty_versions) aktiviert. Beispiel:
  * Mit dem {{site.data.keyword.Bluemix_notm}}-CLI-Tool:
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_MONTHLY true
    ```
    {: .codeblock}

  * Alternativ können Sie in der Datei `manifest.yml` Folgendes angeben:
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
          IBM_LIBERTY_MONTHLY: true
    ```

    ```
      env:
          JBP_CONFIG_LIBERTY: "[version: +, app_archive: {features: [javaee-8.0]}]"
          IBM_LIBERTY_MONTHLY: true
    ```
    {: .codeblock}

Wenn Sie die monatliche Laufzeit für eine vorhandene Anwendung aktivieren, ist es möglicherweise erforderlich, die Anwendung zu löschen und erneut mit einer Push-Operation bereitzustellen, nachdem die Umgebungsvariablen festgelegt wurden. 
