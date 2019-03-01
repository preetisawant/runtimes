---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Buildpack-Standardwerte
{: #buildpack_defauts}

Das Liberty-Buildpack wird in {{site.data.keyword.Bluemix}} häufig aktualisiert. Jedes Release kann Sicherheitskorrekturen oder Feature-Erweiterungen enthalten.

Das Buildpack besitzt die Standardwerte für Einstellungen wie z. B. die Java-Version
oder das Liberty-Feature-Set für WAR- oder EAR-Anwendungen. Einige der Standardwerte können von einem Buildpack-Release zum nächsten geändert werden, wodurch die
Anwendung beeinträchtigt werden kann. Um zu verhindern, dass die Anwendung durch Änderungen an den Buildpackstandardwerten
beeinträchtigt wird, führen Sie die entsprechenden Schritte durch, um Ihre Anwendung so zu konfigurieren, dass
nicht auf die Buildpackstandardwerte zurückgegriffen werden muss.

## Liberty-Versionen
{: #liberty_versions}

Das Buildpack stellt zwei Versionen der Liberty-Laufzeit bereit:
1. Ein langfristiges, stabiles Release
  * Dies ist die Standard-Liberty-Laufzeit.
  * Es stellt keine [Beta-Features](/docs/runtimes/liberty/usingBetaFeatures.html) bereit.
  * Es wird normalerweise vierteljährlich aktualisiert.

2. Das monatliche Release
  * Es muss durch Festlegen des Werts **"version: +"** für die Umgebungsvariable **JBP_CONFIG_LIBERTY** und des Werts **true**
  für die Umgebungsvariable **IBM_LIBERTY_MONTHLY** explizit aktiviert werden. 
  * Es stellt [monatliche Features](/docs/runtimes/liberty/usingMonthlyRuntime.html) bereit. 
  * Es wird normalerweise alle vier Wochen aktualisiert. 

## Liberty-Features
{: #liberty_features}

Wenn Sie WAR- oder EAR-Dateien bereitstellen, wird
vom Buildpack eine Konfiguration mit einem Standardset von Liberty-Features für die Anwendung bereitgestellt. Auch wenn es
selten der Fall ist, kann es sein, dass das Standardset von Liberty-Features von einem Buildpack-Release zum nächsten
geändert wird. Änderungen am Standard-Feature-Set können sich nachteilig auf die Anwendung auswirken. Es gibt jedoch Optionen,
mit denen Sie sicherstellen können, dass die Anwendung nicht durch Änderungen an den Feature-Standardwerten beeinträchtigt
wird.

* Legen Sie die Umgebungsvariable JBP_CONFIG_LIBERTY so fest, dass sie explizit eine Liste aktivierter Features für die
Anwendung angibt. Weitere Informationen finden Sie in [Eigenständige Anwendungen](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps).
* Stellen Sie Ihre Anwendung als
[Serververzeichnis](/docs/runtimes/liberty/optionsForPushing.html#server_directory) oder
[paketierten Server](/docs/runtimes/liberty/optionsForPushing.html#packaged_server) bereit. Passen Sie die Datei 'server.xml' so an, dass sie das exakte für Ihre Anwendung benötigte Feature-Set enthält, und stellen Sie sie bereit.

Anwendungen, die als Serververzeichnis oder
paketierter Server bereitgestellt werden, werden durch Änderungen an den Liberty-Featurestandardwerten nicht beeinträchtigt.

## Java-Version
{: #java_version}

Das Buildpack stellt eine Standard-JRE für die Anwendung bereit. Die übergeordnete oder untergeordnete Version der JRE kann von einem Buildpack-Release zum nächsten geändert werden. Die untergeordnete Version der JRE wird möglicherweise häufig aktualisiert,
während die übergeordnete Version nur selten aktualisiert wird. Änderungen an der übergeordneten Version der JRE können sich nachteilig auf die Anwendung auswirken.

Damit sichergestellt ist, dass die Anwendung nicht durch Änderungen an der übergeordneten Version beeinträchtigt wird, legen Sie die Umgebungsvariable wie in [JRE anpassen](/docs/runtimes/liberty/customizingJRE.html) beschrieben auf die entsprechende JRE-Version fest. Die besten Ergebnisse erzielen Sie, wenn Sie für Ihre Anwendungen Java 8 verwenden.
