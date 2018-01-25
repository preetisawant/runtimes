---

copyright:
  years: 2015, 2017
lastupdated: "2017-12-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Protokollierung und Tracing konfigurieren
{: #logging_tracing}

## Protokolldateien
{: #log_files}

Die Liberty-Standardprotokolle wie `messages.log` oder das Verzeichnis `ffdc` stehen unter {{site.data.keyword.Bluemix}} im Verzeichnis `logs` jeder Anwendungsinstanz zur Verfügung. Auf diese Protokolle kann über die Konsole von {{site.data.keyword.Bluemix_notm}} oder über die Cloud Foundry-CLI zugegriffen werden. Beispiel:

* Um auf die aktuellen Protokolle für eine App zuzugreifen, führen Sie den folgenden Befehl aus:

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* Um die Datei `messages.log` einer App anzuzeigen, die auf einem DEA-Knoten ausgeführt wird, führen Sie den folgenden Befehl aus:

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* Um die Datei `messages.log` einer App anzuzeigen, die in einer Diego-Zelle ausgeführt wird, führen Sie den folgenden Befehl aus:

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

Die Protokollebene und weitere Traceoptionen können in der Liberty-Konfigurationsdatei definiert werden. Weitere Informationen hierzu finden Sie unter [Fehlerbehebung für Liberty: Protokollierung und Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html). Das Tracing kann mithilfe der Konsole von {{site.data.keyword.Bluemix_notm}} auch in einer aktiven Anwendungsinstanz angepasst werden.

## Trace- und Speicherauszugsfunktionen verwenden
{: #using_trace_and_dump}

Die Liberty-Tracekonfiguration kann für die Ausführung einer Anwendung direkt über die Konsole von {{site.data.keyword.Bluemix_notm}} angepasst werden. Die Konsole bietet ferner die Funktion zur Abfrage und zum Herunterladen von Thread- und Heapspeicherauszügen. Um die Tracekonfiguration anzupassen oder um einen Speicherauszug anzufordern, wählen Sie eine Liberty-Anwendung in der Konsole von {{site.data.keyword.Bluemix_notm}} aus und dann das Menü `Laufzeit` in der Navigation. Wählen Sie in der Ansicht `Laufzeit` eine Instanz aus und drücken Sie die Taste für *TRACE* oder *SPEICHERAUSZUG*. Wenn Sie die Tracestufe anpassen, finden Sie Informationen zu Syntaxdetails der Tracespezifikation unter [Fehlerbehebung für Liberty: Protokollierung und Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html).

### Tracekonfiguration über SSH in Diego ändern

Für eine Liberty-Anwendung, die in einer Diego-Zelle ausgeführt wird, können Sie die Tracekonfiguration über die Cloud Foundry-CLI unter Verwendung der SSH-Funktion ändern.

Die Push-Anwendung muss eine server.xml-Datei enthalten, deren Wert für **updateTrigger** auf **polled** gesetzt ist. Auf diese Weise werden Änderungen an der Tracespezifikation in server.xml erkannt und von der Laufzeitumgebung angewendet.

Informationen über Optionen zum Durchführen von Push-Operationen für Liberty-Apps mit einer angepassten server.xml-Datei finden Sie unter [Optionen zur Durchführung von Push-Operationen für Liberty-Apps](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing).

Informationen zum Einrichten der dynamischen Aktualisierung in der server.xml-Datei finden Sie unter [Dynamische Aktualisierungen steuern](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window}. 

Führen Sie zum Ändern der Tracekonfiguration die folgenden Schritte aus:

1. Greifen Sie über SSH auf Ihre App zu.

  ```
$ cf ssh <appname> [-i instance_index]
  ```
  {: pre}

2. Bearbeiten Sie ```<logging traceSpecification="xxxx"/>``` in der server.xml-Datei entsprechend, um die gewünschte Tracespezifikation festzulegen, beispielsweise mithilfe von *vi*:

  ```
$ vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: pre}

Hinweis: Die Änderung der server.xml-Datei geht bei einem erneuten Staging oder einem Neustart verloren und gilt nur für die Instanz, auf die Sie über SSH zugreifen.

Detaillierte Informationen zur Syntax der Tracespezifikation finden Sie unter [Fehlerbehebung für Liberty: Protokollierung und Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window}.

### Speicherauszüge in Diego über SSH auslösen

Für eine Anwendung, die in einer Diego-Zelle ausgeführt wird, können Sie einen Thread und einen Heapspeicherauszug über die CF-CLI unter Verwendung der SSH-Funktion auslösen. Beispiel:

  ```
$ cf ssh <appname> -c "pkill -3 java"
  ```
  {: pre}

Details zum Herunterladen der generierten Speicherauszugsdateien finden Sie in der Dokumentation unten.

## Speicherauszugsdateien herunterladen
{: #download_dumps}

Verschiedene Speicherauszugsdateien werden standardmäßig im Verzeichnis `dumps` des Anwendungscontainers gespeichert.

### DEA-Anwendung

Bei einer Anwendung, die auf einem DEA-Knoten ausgeführt wird, verwenden Sie die Funktion "cf files", um die Speicherauszugsdateien anzuzeigen und herunterzuladen.

* Um die generierten Speicherauszüge anzuzeigen, führen Sie den folgenden Befehl aus:

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* Um eine Speicherauszugsdatei herunterzuladen, führen Sie die folgenden Befehle aus:

    1. Anwendungs-GUID abrufen

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. Speicherauszugsdatei herunterladen

      ```
      $ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
      ```
      {: codeblock}

### Diego-Anwendung

Bei einer Anwendung, die in einer Diego-Zelle ausgeführt wird, verwenden Sie die Funktion "cf ssh", um die Speicherauszugsdatei anzuzeigen und herunterzuladen.

* Um die generierten Speicherauszüge anzuzeigen, führen Sie den folgenden Befehl aus:

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Um eine Speicherauszugsdatei herunterzuladen, führen Sie folgenden Befehl aus:

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

Es ist auch möglich, `scp` und andere ähnliche Tools zu verwenden, um die Speicherauszugsdateien anzuzeigen und herunterzuladen. Weitere Informationen finden Sie unter [Accessing Apps with SSH ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html).

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Liberty-Laufzeit](index.html)
* [Übersicht über Liberty](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
