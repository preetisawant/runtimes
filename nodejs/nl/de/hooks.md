---

copyright:
  years: 2018
lastupdated: "2018-11-09"
subcollection: "Nodejs"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# Services anderer Anbieter mit Hooks integrieren
{: #hooks}

Mithilfe von Hooks können Sie Services anderer Anbieter unkompliziert in das SDK for Node.js-Buildpack integrieren. Beachten Sie, dass IBM keine Unterstützung für Services anderer Anbieter bereitstellt, die Sie integrieren. Weitere Informationen zur Unterstützung finden Sie im Abschnitt zu den [Services anderer Anbieter](/docs/runtimes-common/buildpackSupport.html#third-party).

Im SDK for Node.js-Buildpack ist der Dynatrace-Hook enthalten. Dynatrace ermöglicht die Anwendungsüberwachung von Node.js-Anwendungen. Weitere Informationen zur Verwendung des Dynatrace-Hooks im Buildpack finden Sie in der [Dynatrace-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")]( https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/application-only/deploy-oneagent-on-cloud-foundry-for-application-only-monitoring/){: new_window}.


Beachten Sie beim Befolgen von Anweisungen in der Dokumentation anderer Anbieter, dass Sie den Befehl `ibmcloud cf` und nicht den Befehl `cf` zum Ausführen von Befehlen für Ihr {{site.data.keyword.Bluemix_notm}}-Buildpack verwenden.
{: tip}
