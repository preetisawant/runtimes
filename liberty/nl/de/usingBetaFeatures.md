---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-19"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Beta-Features verwenden
{: #using_beta_features}

Die Beta-Features von Liberty ermöglichen den vorzeitigen Zugriff auf die neuen Funktionen und Programmiermodelle, die in einem zukünftigen Liberty-Release enthalten sein können. Die meisten Beta-Features können auch in Anwendungen verwendet werden, die in {{site.data.keyword.Bluemix}} implementiert sind.

**Wichtig:** Die Beta-Features dienen nur zu Entwicklungs- und Testzwecken und können in Produktionsumgebungen nicht verwendet werden. Umfassende Nutzungsbedingungen finden Sie in der [Lizenzvereinbarung für Betaversionen](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

| Features |
| ------ |
| `logstashCollector-1.1` |
| `validator-1.0` |
{: caption="Tabelle 1. In Liberty for Java verfügbare Liberty-Beta-Features in {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

Zur Verwendung der Liberty-Beta-Features in {{site.data.keyword.Bluemix_notm}} müssen Sie wie folgt vorgehen:

1. [Implementieren Sie ein Serververzeichnis oder einen paketierten Server](optionsForPushing.html) mit einem oder mehreren in der Datei 'server.xml' aktivierten Beta-Features, wie im folgenden Beispiel gezeigt:

  ```
<server>
    <featureManager>
        <feature>logstashCollector-1.1</feature>
    </featureManager>
</server>
  ```
  {: .codeblock}

2.  Setzen Sie die Umgebungsvariable `IBM_LIBERTY_BETA` auf `true`. Diese Variable weist das Liberty-Buildpack an, die Beta-Features zu installieren und für Ihre Anwendung zu aktivieren.  Beispiel:
  * Über die [{{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle](../../cli/reference/bluemix_cli/download_cli.html):
    ```
    ibmcloud cf set-env <yourappname> IBM_LIBERTY_BETA true
    ```
    {: .codeblock}

  * Alternativ können Sie in der Datei `manifest.yml` Folgendes angeben:
    ```
      env:
          IBM_LIBERTY_BETA: "true"
    ```
    {: .codeblock}

3. Setzen Sie die Umgebungsvariable `JBP_CONFIG_LIBERTY` auf `"version: +"`. Diese Variable aktiviert die [monatliche Liberty-Laufzeit](buildpackDefaults.html#liberty_versions), die Beta-Features unterstützt. Beispiel:
  * Mit dem {{site.data.keyword.Bluemix_notm}}-CLI-Tool:
    ```
    ibmcloud cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
    ```
    {: .codeblock}

  * Alternativ können Sie in der Datei `manifest.yml` Folgendes angeben:
    ```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
    ```
    {: .codeblock}

Wenn Sie die Beta-Features für eine bestehende Anwendung aktivieren, müssen Sie für Ihre Anwendung nach dem Einstellen der Umgebungsvariablen ein erneutes Staging durchführen.
