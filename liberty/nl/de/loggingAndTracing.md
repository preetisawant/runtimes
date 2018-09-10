---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Protokollierung und Tracing konfigurieren
{: #logging_tracing}

## Protokolldateien
{: #log_files}

Die Liberty-Standardprotokolle wie `messages.log` oder das Verzeichnis `ffdc` stehen unter {{site.data.keyword.Bluemix}} im Verzeichnis `logs` jeder Anwendungsinstanz zur Verfügung. Auf diese Protokolle kann über die {{site.data.keyword.Bluemix_notm}}-Konsole oder über die {{site.data.keyword.Bluemix_notm}}-CLI zugegriffen werden. Beispiel:

* Um auf die aktuellen Protokolle für eine App zuzugreifen, führen Sie den folgenden Befehl aus:

  ```
  ibmcloud cf logs --recent <appname>
  ```
  {: codeblock}


* Zum Anzeigen der Datei `messages.log` einer App führen Sie den folgenden Befehl aus:

  ```
  ibmcloud cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

Die Protokollebene und weitere Traceoptionen können in der Liberty-Konfigurationsdatei definiert werden. Weitere Informationen hierzu finden Sie unter [Fehlerbehebung für Liberty: Protokollierung und Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html).

## Trace- und Speicherauszugsfunktionen verwenden
{: #using_trace_and_dump}

### Trace und Speicherauszug in der {{site.data.keyword.Bluemix_notm}}-Konsole verwenden (veraltet)

Die Liberty-Tracekonfiguration kann für die Ausführung einer Anwendung direkt über die {{site.data.keyword.Bluemix_notm}}-Konsole angepasst werden. Die Konsole bietet ferner die Funktion zur Abfrage und zum Herunterladen von Thread- und Heapspeicherauszügen. Um die Tracekonfiguration anzupassen oder um einen Speicherauszug anzufordern, wählen Sie eine Liberty-Anwendung in der {{site.data.keyword.Bluemix_notm}}-Konsole und dann das Menü `Laufzeit` in der Navigation aus. Wählen Sie in der Ansicht `Laufzeit` eine Instanz aus und klicken auf die Schaltfläche für *TRACE* oder *SPEICHERAUSZUG*. Wenn Sie die Tracestufe anpassen, finden Sie Informationen zu Syntaxdetails der Tracespezifikation unter [Fehlerbehebung für Liberty: Protokollierung und Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html).

### Tracekonfiguration über SSH ändern

Wenn Sie eine Push-Operation für die Anwendung durchführen, enthält die Datei 'server.xml' die Standardeigenschaften **updateTrigger** mit dem Wert **polled** und **monitorInterval** mit dem Wert 1 Minute. Der Liberty-Server wurde automatisch so konfiguriert, dass er jede Minute die Datei 'server.xml' auf Aktualisierungen überprüft.

Informationen über Optionen zum Durchführen von Push-Operationen für Liberty-Apps mit einer angepassten Datei `server.xml` finden Sie unter [Optionen zur Durchführung von Push-Operationen für Liberty-Apps](https://console.ng.bluemix.net/docs/runtimes/liberty/optionsForPushing.html#options_for_pushing).

Informationen zum Einrichten der dynamischen Aktualisierung in der Datei 'server.xml' finden Sie unter [Dynamische Aktualisierungen steuern](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/twlp_setup_dyn_upd.html){: new_window}.

Führen Sie die folgenden Schritte aus, um die Tracekonfiguration zu zu ändern:

1. Greifen Sie über SSH auf Ihre App zu.

  ```
 ibmcloud cf ssh <appname> [-i instance_index]
  ```
  {: codeblock}

2. Bearbeiten Sie `<logging traceSpecification="xxxx"/>` in der Datei 'server.xml' entsprechend, um die gewünschte Tracespezifikation festzulegen, zum Beispiel mit *vi*:

  ```
vi /app/wlp/usr/servers/defaultServer/server.xml
  ```
  {: codeblock}

Hinweis: Die Änderung der Datei 'server.xml' geht bei einem erneuten Staging oder einem Neustart verloren und gilt nur für die Instanz, auf die Sie über SSH zugreifen.

Detaillierte Informationen zur Syntax der Tracespezifikation finden Sie unter [Fehlerbehebung für Liberty: Protokollierung und Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html){: new_window}.

### Speicherauszüge über SSH auslösen

Verwenden Sie den folgenden Befehl, um einen Thread- und Heapspeicherauszug mit dem Feature SSH über die {{site.data.keyword.Bluemix_notm}}-CLI auszulösen:

  ```
 ibmcloud cf ssh <appname> -c "pkill -3 java"
  ```
  {: codeblock}

Details zum Herunterladen der generierten Speicherauszugsdateien finden Sie in der folgenden Dokumentation.

## Speicherauszugsdateien herunterladen
{: #download_dumps}

Verschiedene Speicherauszugsdateien werden standardmäßig im Verzeichnis `dumps` des Anwendungscontainers gespeichert. Verwenden Sie den {{site.data.keyword.Bluemix_notm}}-CLI-Befehl `ibmcloud cf ssh`, um die Speicherauszugsdateien anzuzeigen und herunterzuladen.

* Um die generierten Speicherauszüge anzuzeigen, führen Sie den folgenden Befehl aus:

  ```
  ibmcloud cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Um eine Speicherauszugsdatei herunterzuladen, führen Sie folgenden Befehl aus:

  ```
  ibmcloud cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

Es ist auch möglich, `scp` und andere ähnliche Tools zu verwenden, um die Speicherauszugsdateien anzuzeigen und herunterzuladen. Weitere Informationen finden Sie unter [Accessing Apps with SSH ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html).

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Liberty-Laufzeit](index.html)
* [Übersicht über Liberty](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
