---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Beta-Features verwenden
{: #using_beta_features}

Die Beta-Features von Liberty ermöglichen den vorzeitigen Zugriff auf die neuen Funktionen und Programmiermodelle, die in einem zukünftigen Liberty-Release enthalten sein können. Die meisten Beta-Features können auch in Anwendungen verwendet werden, die in {{site.data.keyword.Bluemix}} implementiert sind.

**Wichtig**: Die Beta-Features dienen nur zu Entwicklungs- und Testzwecken und dürfen in Produktionsumgebungen nicht verwendet werden. Umfassende Nutzungsbedingungen finden Sie in der
[ Lizenzvereinbarung für Betaversionen](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

In {{site.data.keyword.Bluemix_notm}} verfügbare Liberty-Beta-Features
<table>
<tr>
<th align="left">Features</th>
</tr>

<tr>
    <tr><td>appSecurity-3.0</tr></td>
    <tr><td>audit-1.0</tr></td>
    <tr><td>beanValidation-2.0</tr></td>
    <tr><td>bluemixLogCollector-1.1</tr></td>
    <tr><td>cdi-2.0</tr></td>
    <tr><td>javaee-8.0</tr></td>
    <tr><td>javaeeClient-8.0</tr></td>
    <tr><td>jaxrs-2.1</tr></td>
    <tr><td>jpa-2.2</tr></td>
    <tr><td>jpaContainer-2.2</tr></td>
    <tr><td>jsf-2.3</tr></td>
    <tr><td>jsfContainer-2.2</tr></td>
    <tr><td>jsonb-1.0</tr></td>
    <tr><td>jsonbContainer-1.0</tr></td>
    <tr><td>jsonp-1.1</tr></td>
    <tr><td>jsonpContainer-1.1</tr></td>
    <tr><td>logstashCollector-1.1</tr></td>
    <tr><td>mpConfig-1.2</tr></td>
    <tr><td>mpOpenAPI-1.0</tr></td>
    <tr><td>mpRestClient-1.0</tr></td>
    <tr><td>opentracing-1.0</tr></td>
    <tr><td>servlet-4.0</tr></td>
    <tr><td>validator-1.0</tr></td>
    <tr><td>webProfile-8.0</tr></td>

</tr>
</table>

Führen Sie die folgenden Schritte aus, um die Liberty-Beta-Features in {{site.data.keyword.Bluemix_notm}} verwenden zu können:

1. [Implementieren Sie ein Serververzeichnis oder einen paketierten Server](optionsForPushing.html) mit mindestens einem in der Datei 'server.xml' aktivierten Beta-Feature, wie im folgenden Beispiel gezeigt:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>mpOpenAPI-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Setzen Sie die Umgebungsvariable **IBM_LIBERTY_BETA** auf **true**. Diese Variable weist das
Liberty-Buildpack an, die Beta-Features zu installieren und für Ihre Anwendung zu aktivieren.  Beispiel:
  * Verwendung des Befehlszeilentools 'cf':
```
       $ cf set-env <yourappname> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * Alternativ Verwendung der Datei 'manifest.yml':
```
      env:
          IBM_LIBERTY_BETA: "true"
```

3. Setzen Sie die Umgebungsvariable **JBP_CONFIG_LIBERTY** auf **"version: +"**. Diese Variable aktiviert die [monatliche Liberty-Laufzeit](buildpackDefaults.html#liberty_versions), die Beta-Features unterstützt. Beispiel:
  * Verwendung des Befehlszeilentools 'cf':
```
       $ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * Alternativ Verwendung der Datei 'manifest.yml':
```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
```

Wenn Sie die Beta-Features für eine bestehende Anwendung aktivieren, müssen Sie für Ihre Anwendung nach dem Einstellen der Umgebungsvariablen ein erneutes Staging durchführen.

{: #codeblock}

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Liberty for Java-Laufzeit](index.html)
* [Übersicht über Liberty](https://www.ibm.com/support/knowledgecenter/SSAW57_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/cwlp_about.html)
