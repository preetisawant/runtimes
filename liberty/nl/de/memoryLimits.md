---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-14"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Speicherbegrenzungen und das Liberty-Buildpack
{: #memory_limits}

Bei der Implementierung einer Anwendung mit dem Liberty-Buildpack muss eine
Speicherbegrenzung angegeben werden.

## Speicherbegrenzungen und das Liberty-Buildpack
{: #memory_limits_and_liberty}


Bei der Implementierung einer Anwendung mit dem Liberty-Buildpack werden Sie zur Eingabe einer Speicherbegrenzung aufgefordert. Das Liberty for Java-Buildpack legt einen standardmäßigen Faktor für die Größe des Heapspeichers fest um zu verhindern, dass der Prozess die Speicherbegrenzung überschreitet. Sie können die Größe des Heapspeichers oder den Größenfaktor auch angeben, indem Sie die Umgebungsvariable `JVM_ARGS` oder `JBP_CONFIG_IBMJDK` definieren. Weitere Informationen finden Sie unter [Heapspeicheroptionen](#heap_memory_options).

Um den richtigen Wert für die Speicherbegrenzung zu bestimmen, müssen Sie sich
darüber im Klaren sein, dass Sie nicht die Größe des Java-Anwendungsheapspeichers angeben. Sie geben die Speicherkapazität an, die für den zu verwendenden Diego-Container oder DEA verfügbar ist. Dieser Wert schließt den von den
folgenden Komponenten verwendeten Speicher ein:

* Warden-Container.
* Speicher, der für die Zuordnung von Kernelerweiterungen und Systembibliotheken zum Prozess verwendet wird.
* Speicher, der für die ausführbaren JVM-Dateien, den JVM-Arbeitsheapspeicher, den JIT-Bereich und komprimierte Referenzen verwendet wird.
* Speicher, der für Klassen (Anwendungsserver und Anwendung), Thread-Stacks und direkte E/A-Puffer verwendet wird.
* Heapspeicher der Java-Anwendung.

Weitere Informationen zur JVM-Speicherbelastung finden Sie im developerWorks-Artikel [Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/).

Wenn
Sie eine Anwendung implementieren, wird die Speicherbelegung des gesamten Prozesses
überwacht. Wenn die Speicherbelegung die bei der Implementierung der Anwendung angegebene Speicherbegrenzung
überschreitet, stoppt der Kernel den Prozess. Diese Maßnahme erfolgt ohne Warnung und kann sich auf unterschiedliche Weise auswirken:

 Wenn die Speicherbegrenzung während der Anwendungsbereitstellung überschritten wird, empfangen Sie eine Nachricht mit dem Hinweis, dass ein Fehler aufgetreten ist und es tritt möglicherweise eine der folgenden Möglichkeiten ein.

  * Es könnte zu einem Flapping
der Anwendung kommen. 
  * Oder Sie stellen fest, dass die Anwendung mehrere erfolglose Startversuche
unternommen hat. 
  * Sie empfangen möglicherweise eine Nachricht mit dem Hinweis, dass die Anwendungsbereitstellung fehlgeschlagen ist.

Wenn die Speicherbegrenzung überschritten wird, während die Anwendung aktiv ist, wird der Prozess gestoppt und Cloud Foundry versucht, die Anwendung erneut zu starten. Der Neustart der Anwendung kann erfolgen, die Anwendung ist aber für eine gewisse Zeit nicht verfügbar.

## Heapspeicheroptionen
{: #heap_memory_options}

Sie können auf unterschiedliche Weise den Maximalwert für den Heapspeicher anpassen, der Ihrer Anwendung zugeordnet ist. Sie können die Umgebungsvariable `JVM_ARGS` verwenden, die Datei `jvm.options` ändern oder die Umgebungsvariable `JBP_CONFIG_IBMJDK` festlegen, die `heap_size_ratio` steuert. Wenn Sie keine Einstellungen angeben, verwendet das Buildpack die Standardeinstellungen.

### Heapspeicher - Standardwerte
{: .#heap_memory_defaults}
Um Fehler zu vermeiden, die durch das Überschreiten von Speicherbegrenzungen verursacht werden, legt das Liberty for Java-Buildpack einen standardmäßigen Faktor für die Größe des Heapspeichers in Abhängigkeit der von Ihnen bei der Bereitstellung der Anwendung angegebenen Speicherbegrenzung fest.

* Anwendungen mit Speicherbegrenzungen von weniger als 512M verfügen über einen Faktor für die Größe des Heapspeichers von 50%
* Anwendungen mit Speicherbegrenzungen größer-gleich 512M verfügen über einen Faktor für die Größe des Heapspeichers von 75%

Wenn Sie den Heapspeicher mithilfe von Umgebungsvariablen angeben, setzen Sie die standardmäßigen Faktoren für die Größe des Heapspeichers außer Kraft.

### Heapspeicher angeben
{: #specifying_heap_memory}

Sie können die Größe des Heapspeichers mithilfe von Umgebungsvariablen oder durch Ändern der Datei `jvm.options` festlegen. Wenn Sie die Umgebungsvariable `JVM_ARGS` oder `JBP_CONFIG_IBMJDK` verwenden, werden sämtliche Änderungen wirksam, wenn Ihre Anwendung mit Push-Operation nach Bluemix übertragen wird. Beim Ändern der Datei `jvm.options` kann die Auswirkung auf die Konfiguration der Heapspeichergröße auch lokal getestet werden.

* Verwenden Sie die Umgebungsvariable `JVM_ARGS` und das Argument -Xmx. Um beispielsweise die maximale Größe des Heapspeichers auf 512M zu setzen, geben Sie den folgenden Befehl ein und
führen anschließend ein erneutes Staging Ihrer App durch. 

```
    $ cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* Geben Sie den Faktor für die Größe des Heapspeichers mithilfe der Umgebungsvariablen JBP_CONFIG_IBMJDK an. Der Gleitkommawert heap_size_ratio gibt an, wie viel Speicher der Speicherbegrenzung dem Heapspeicher zugeordnet wird. Um beispielsweise die Hälfte des verfügbaren Speichers dem Heapspeicher zuzuordnen (50% oder 0.50), setzen Sie den folgenden Befehl ab und führen anschließend ein erneutes Staging Ihrer App durch.

```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}

* Geben Sie das Argument -Xmx in der Datei jvm.options an, wenn Ihre Anwendung ein [Serververzeichnis](optionsForPushing.html#server_directory) oder ein [paketierter Server](optionsForPushing.html#packaged_server) ist. Weitere Informationen zur Verwendung der Datei `jvm.options` mit der Liberty-Laufzeit finden Sie unter [Setting generic JVM](http://www-01.ibm.com/support/docview.wss?uid=swg21596474).  
