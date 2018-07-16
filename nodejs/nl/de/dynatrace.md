---

copyright:
  years: 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dynatrace zur Überwachung von Node.js in {{site.data.keyword.cloud_notm}} verwenden
{: #using_dynatrace}

Bei Dynatrace handelt es sich um einen Service eines anderen Anbieters, der Überwachungsmetriken für Ihre App bereitstellt. Sie können Dynatrace in Ihre Node.js-Anwendung integrieren, jedoch stellt IBM keine Unterstützung für Services anderer Anbieter bereit. Weitere Informationen finden Sie unter [Services anderer Anbieter](../common/buildpackSupport.html#third-party).

Informationen zu Dynatrace sowie zur zugehörigen Lizenzierung finden Sie unter [Dynatrace-Anwendungsüberwachung![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.dynatrace.com/en/products/application-monitoring.html).

Wenn Ihre Node.js-Anwendung für die Verwendung von Dynatrace konfiguriert ist, fordert die Node.js-Laufzeit von einer Dynatrace-Site eine Dynatrace-Plattform als PaaS-Installationsscript (PaaS - Platform as a Service) an und führt diesen Dynatrace-Agenten mit Ihrer App aus. Für die Integration von Dynatrace in Ihre App müssen Sie einen vom Benutzer zur Verfügung gestellten Service erstellen und den Service anschließend an Ihre App binden.

## Dynatrace in die Anwendung integrieren

1. Melden Sie sich bei Ihrem Dynatrace-Konto an und generieren Sie ein PaaS-Token. Informationen dazu finden Sie im Abschnitt zum [Generieren eines PaaS-Tokens ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/how-do-i-monitor-cloud-foundry-applications/) in der Dokumentation zur Dynatrace-Überwachung von Cloud Foundry-Apps.

  Notieren Sie sich Ihre Umgebungs-ID und das Token.
1. Erstellen Sie einen vom Benutzer zur Verfügung gestellten Service, der auf Ihre Dynatrace-Berechtigungsnachweise verweist, indem Sie den folgenden Befehl ausführen. Der Name des Service muss die Zeichenfolge `dynatrace` enthalten, zum Beispiel `dynatrace-service`.

    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken"
    ```
    {: codeblock}
    
    **Hinweis:** Ersetzen Sie `environmentid` oder `apitoken` nicht durch Ihre Berechtigungsnachweise. Wenn Sie den Befehl ausführen, werden Sie aufgefordert, Werte für sie einzugeben.

    Wenn Sie Dynatrace Managed verwenden, fügen Sie außerdem das Feld `apiurl` hinzu, das den API-Endpunkt Ihres verwalteten Servers (Managed Server) angibt.
    
    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken, apiurl"
    ```
    {: codeblock}
    
    Wenn Sie beim Ausführen des Befehls dazu aufgefordert werden, geben Sie für das Feld `apiurl` den Wert `https://<YourManagedServerURL>/e/<environmentID>/api` an.
    
1. Übertragen Sie Ihre App mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}} und binden Sie den vom Benutzer zur Verfügung gestellten Service, den Sie erstellt haben, anschließend an die App. Verwenden Sie zum Beispiel den folgenden Befehl:
    ```
    ibmcloud cf bs myApp dynatrace-service
    ```
    {: codeblock}

    **Hinweis:** Sie müssen nach dem Binden des Service ein erneutes Staging für Ihre Anwendung durchführen.

   Alternativ können Sie den Service an Ihre App binden, indem Sie den Namen Ihres vom Benutzer zur Verfügung gestellten Service im Abschnitt `service` der Datei `manifest.yml` Ihrer App hinzufügen.
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
