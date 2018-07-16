---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Eigene JRE verwenden
{: #using_own_jre}

Sie können Ihre Liberty-Anwendung in {{site.data.keyword.Bluemix}} mit Ihrer eigenen JRE (Java Runtime Environment) verwenden. Damit Ihre JRE für Ihre Anwendung verfügbar ist, müssen Sie die folgenden Schritte ausführen:
* Die JRE an einer Position hosten, von der sie vom Buildpack heruntergeladen werden kann.
* Eine Datei `index.yml` hosten, die die JRE-Position bereitstellt.
* Ihre Anwendung für die Verwendung Ihrer JRE konfigurieren.

## JRE und `index.yml` hosten
{: #hosting_jre}

Sie müssen die JRE-Datei auf einem Web-Server hosten, von dem das Liberty-Buildpack Dateien herunterladen kann. Sie können die Datei mithilfe einer beliebigen verfügbaren Serverfunktion in {{site.data.keyword.Bluemix_notm}} hosten, oder Sie können sie an einer öffentlich verfügbaren Position hosten. Der Server muss mit der Datei `index.yml` konfiguriert werden, die Details zu der JRE-Datei angibt.

Führen Sie die Schritte aus, die im Folgenden für das Hosten der JRE-Datei und der Datei `index.yml` angegeben sind:
  1. Fordern Sie die JRE an. Dabei muss es sich um eine JRE-Version für ein UNIX-64-Bit-Betriebssystem handeln, die als eine `tar.gz`-Datei vorliegt.
  2. Hosten Sie die JRE-Datei an einer Position, von der das Liberty-Buildpack sie herunterladen kann.
  3. Stellen Sie eine Datei `index.yml` an der Hostingposition bereit. Die Datei `index.yml` muss einen Eintrag enthalten, der eine Versions-ID der JRE umfasst, gefolgt von einem Doppelpunkt und der vollständigen URL der JRE-Dateiposition.
    * Definieren Sie die JRE-Version in der Datei `index.yml`.

    ```
    ---
    jre_version: https://hostingLocation/jreName.tar.gz
    ```
    {: codeblock}

    * Schließen Sie die JRE-Versions-ID sowie die vollständige URL der JRE-Dateiposition ein.  Beispiel:

    ```
    ---
    1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```
    {: codeblock}

## Die App konfigurieren
{: #configure_app}

Sie müssen zwei Umgebungsvariablen in der Liberty-Anwendung festlegen, um das Buildpack zur Verwendung einer alternativen JRE zu konfigurieren. Legen Sie die Umgebungsvariable **JBP_CONFIG_OPENJDK** zur Angabe der Position der Datei `index.yml` fest und die Umgebungsvariable **JVM** für *openjdk*. Weitere Informationen zum Format der Zeichenfolge 'version-value' finden Sie in der Cloud Foundry-Dokumentation unter [Version Syntax and Ordering and Wildcards ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/util-repositories.md){: new_window}.

Der Wert für die Variable **JBP_CONFIG_OPENJDK** ist die Position der Datei `index.yml` und die JRE-Version, die aus der Datei index.yml ausgewählt wird.

```
'{repository_root: "https://locationToIndexYml", version: version-value}'
```
{: codeblock}

Setzen Sie den Befehl `ibmcloud cf se myAPP` ab, um die Variable **JBP_CONFIG_OPENJDK** festzulegen. Beispiel:
```
ibmcloud cf se myApp JBP_CONFIG_OPENJDK '{repository_root: "https://myHostingApp.ng.bluemix.net", version: 1.8.+}'
```
{: codeblock}

Die URL *repository_root* enthält nicht `index.yml` in der URL. Die URL *repository_root* zeigt auf die Verzeichnisebene, die die Datei `index.yml` enthält, nicht auf die Datei selbst.

Setzen Sie zum Festlegen der JVM-Umgebungsvariablen den folgenden Befehl ab:
```
ibmcloud cf se myApp JVM 'openjdk'
```
{: codeblock}

**Hinweis:** Führen Sie nach dem Festlegen der Umgebungsvariablen ein erneutes Staging Ihrer Anwendung aus, damit die Änderungen wirksam werden.

## Bestätigen
{: #confirmation}

Prüfen Sie das Staging-Protokoll zur Bestätigung, dass Liberty die erwartete JRE verwendet. Suchen Sie nach einer Nachricht, die angibt, dass der Server das Buildpack aus der in der Datei `index.yml` angegebenen Position heruntergeladen hat. Das folgende Snippet enthält ein Beispiel der Protokollausgabe, wenn Liberty die erwartete JRE erfolgreich verwendet.
```
 -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}
