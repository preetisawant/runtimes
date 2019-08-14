---

copyright:
  years: 2016, 2018
lastupdated: "2018-06-27"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dynatrace zur Überwachung von Liberty in {{site.data.keyword.cloud_notm}} verwenden
{: #using_dynatrace}

Bei Dynatrace handelt es sich um einen Service eines anderen Anbieters, der Überwachungsmetriken für Ihre App bereitstellt. Sie können Dynatrace in Ihre Liberty-Anwendung integrieren, jedoch stellt IBM keine Unterstützung für Services anderer Anbieter bereit. Weitere Informationen finden Sie unter [Services anderer Anbieter](/docs/runtimes-common/buildpackSupport.html#third-party).

Weitere Informationen zu Dynatrace sowie zur zugehörigen Lizenzierung finden Sie unter [Dynatrace Application Monitoring ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.dynatrace.com/en/products/application-monitoring.html).

Wenn Ihre Liberty-Anwendung für die Verwendung von Dynatrace konfiguriert ist, besteht das Standardverhalten darin,
dass die Liberty-Laufzeit die JAR-Datei (`.jar`) eines Dynatrace-Agenten von einer Dynatrace-Site anfordert
und diesen Dynatrace-Agenten mit Ihrer App ausführt.  Bei diesem Standardverhalten besteht die minimal notwendige Konfiguration für die
Verwendung von Dynatrace im Erstellen eines vom Benutzer zur Verfügung gestellten Service,
der auf Ihren Dynatrace-Kollektor verweist.

## Einen vom Benutzer zur Verfügung gestellten Service erstellen, der auf Ihren Dynatrace-Kollektor verweist

Zunächst müssen Sie einen Dynatrace-Kollektor einrichten.  Dann müssen Sie einen vom Benutzer zur Verfügung gestellten
Service erstellen, um Informationen zu übergeben, damit der Dynatrace-Agent eine Verbindung zum Dynatrace-Kollektor herstellt. Informationen zum besseren Verständnis der Beziehung zwischen Dynatrace-Komponenten finden Sie in der Beschreibung der [Dynatrace-Architektur ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://community.dynatrace.com/community/display/DOCDT65/Architecture).

1. Richten Sie einen Dynatrace-Kollektor ein.
  * Anweisungen zum Herunterladen und Einrichten des Dynatrace-Kollektors finden Sie auf der [Website der Dynatrace-Community ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace).
  * Stellen Sie sicher, dass der Kollektor an einer Position eingerichtet wird, auf die der Dynatrace-Agent, der mit Ihrer App in {{site.data.keyword.Bluemix_notm}} ausgeführt wird, zugreifen kann.
2. Erstellen Sie einen vom Benutzer zur Verfügung gestellten Service, der auf den aktiven Dynatrace-Agenten verweist.

  **Hinweis:** Der Name des vom Benutzer zur Verfügung gestellten Service muss die Zeichenfolge **dynatrace** enthalten. Die Groß-/Kleinschreibung wird ignoriert. Verwenden Sie zum Beispiel den folgenden Befehl, in dem **my-dynatrace-collector** die Zeichenfolge **dynatrace** enthält:
  ```
  ibmcloud cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
  ```
  {: codeblock}

    In diesem Beispiel ist 'my-dynatrace-collector' der angegebene Name des Service, 'DynatraceCollectorIPaddress' ist die IP-Adresse des von Ihnen konfigurierten Dynatrace-Kollektors und 'profile' ist der Name des optionalen Dynatrace-Profils, der dieser überwachten App zugeordnet ist. Der Standardwert für das Profil ist 'Monitoring' (Überwachung). Sie können wie im anschließenden Beispiel optional Parameter angeben.

    ```
    ibmcloud cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                      "options" : {"dynatrace-parameter-1": "value",
                                   "dynatrace-parameter-2": "value"}}'
    ```
    {: codeblock}

    Im Abschnitt zu den [_Agenteneinstellungen_ (Agent Settings) unter 'Agent Configuration' ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://community.dynatrace.com/community/display/DOCDT65/Set+up+Agents) auf der Website der Dynatrace-Community finden Sie weitere Informationen zu verfügbaren Optionen. Beispielsweise können Sie mit der Ausschlussoption Klassen von der Überwachung durch Dynatrace ausnehmen. Weitere Informationen zur Konfiguration des vom Benutzer zur Verfügung gestellten Service finden Sie unter [Dynatrace Agent Framework ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md).

3. Übertragen Sie Ihre App mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}} und binden Sie den vom Benutzer zur Verfügung gestellten Service, den Sie erstellt haben, anschließend an die App. Verwenden Sie zum Beispiel den folgenden Befehl:
  ```
  ibmcloud cf bs myApp my-dynatrace-collector
  ```
  {: codeblock}

    **Hinweis:** Sie müssen nach dem Binden des Service ein erneutes Staging für Ihre Anwendung durchführen.

## Optionale Konfiguration
{: #optional_configuration}

Sie können die `.jar`-Datei des Dynatrace-Agenten selbst anfordern und hosten.  In diesem Fall sind die folgenden
zusätzlichen Konfigurationsschritte erforderlich.
1. Fordern Sie die `.jar`-Datei des Dynatrace-Agenten an und hosten Sie sie, damit das Liberty-Buildpack sie herunterladen kann.
2. Konfigurieren Sie Ihre Liberty-App, damit sie den Dynatrace-Agenten herunterladen kann.

### Dynatrace-Agent hosten
{: #hosting_dynatrace_agent}
Der Dynatrace-Agent muss als Host einen Web-Server haben und das Liberty-Buildpack muss die `.jar`-Datei des Agenten von diesem Server herunterladen können. Der Server muss mit der Datei `index.yml` konfiguriert werden, die Details zu der `.jar`-Datei des Agenten angibt. Führen Sie die Schritte aus, die im Folgenden für die Konfiguration des Dynatrace-Agenten angegeben sind:
  1. Laden Sie die `.jar`-Datei des Dynatrace-Agenten herunter. Anweisungen zum Herunterladen der `.jar`-Datei des Dynatrace-Agenten finden Sie unter [Dynatrace Server Platform Installers ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace) auf der Website der Dynatrace-Community. Die entsprechende `.jar`-Datei des Agenten für die Ausführung in {{site.data.keyword.Bluemix_notm}} ist die Datei **dynatrace-agent-unix.jar** einer Version **6.+**.
  2. Hosten Sie die `.jar`-Datei des Agenten an einer Position, von der das Liberty-Buildpack sie herunterladen kann. Sie können die Datei mithilfe einer beliebigen verfügbaren Serverfunktion in {{site.data.keyword.Bluemix_notm}} selbst hosten oder Sie können sie an einer öffentlich verfügbaren Position hosten.
     * Stellen Sie sicher, dass Sie an der Hostingposition die Datei `index.yml` bereitstellen. Die Datei `index.yml` muss einen Eintrag enthalten, der aus der Versions-ID der `.jar`-Datei des Agenten besteht, auf die ein Doppelpunkt und die vollständige URL der Position folgt, an der sich diese `.jar`-Datei des Agenten befindet. Beispiel:

            ---
               6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
            {: codeblock}

     * Die Datei **dynatrace-agent-6.3.0-unix.jar** muss an der Position verfügbar sein, die in der Datei `index.yml` angegeben ist. Die `.jar`-Datei und die Datei `index.yml` können als Position dasselbe Verzeichnis haben.

### Liberty-App konfigurieren
{: #configuring_liberty_app}

Die zu überwachende Liberty-App muss konfiguriert werden, sodass sie nach der `.jar`-Datei des Agenten sucht, die Sie zuvor eingerichtet haben. Sie können die App mit der Umgebungsvariablen **JBP_CONFIG_DYNATRACEAPPMONAGENT** konfigurieren. Die Umgebungsvariable **JBP_CONFIG_DYNATRACEAPPMONAGENT** weist das Buildpack an, von welcher Position der Dynatrace-Agent herunterzuladen ist. Führen Sie zum Festlegen der Umgebungsvariablen folgende Schritte aus:

1. Legen Sie die Variable **JBP_CONFIG_DYNATRACEAPPMONAGENT** fest, sodass sie folgenden Wert aufweist: *"repository_root: URL_of_server_hosting_index.yml"*. Setzen Sie beispielsweise folgenden Befehl ab, nachdem Sie für Ihre Anwendung eine Push-Operation durchgeführt haben:

        ibmcloud cf se myApp JBP_CONFIG_DYNATRACEAPPMONAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
        {: codeblock}

    In diesem Beispiel ist *my-dynatrace-agent-host.mybluemix.net* die URL der Datei `index.yml`, die vom Server gehostet wird, den sie zuvor konfiguriert haben.

2. Führen Sie nach dem Festlegen der Umgebungsvariablen ein erneutes Staging für Ihre App durch. Überprüfen Sie das Staging-Protokoll, um eine Nachricht zu finden, in der gemeldet wird, dass der Dynatrace-Agent erfolgreich von dem Server heruntergeladen wurde, der den Agenten hostet. Beispiel:
```
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
```
{: codeblock}
