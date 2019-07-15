---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Esegui l'applicazione Node.js localmente
{: #hints}

Imposta un numero di porta per eseguire la tua applicazione Node.js localmente per non causare conflitti quando viene eseguita su {{site.data.keyword.Bluemix}}.
{: shortdesc}

Quando l'applicazione è in esecuzione su {{site.data.keyword.Bluemix_notm}}, la variabile di ambiente PORT è assegnato da Cloud Foundry. Tuttavia, quando l'applicazione è in esecuzione in locale, PORT non è definita, per cui puoi definire la porta per la tua applicazione. Per evitare conflitti, definisci la porta su cui è in ascolto la tua applicazione localmente con qualcosa di diverso rispetto alla porta utilizzata da {{site.data.keyword.Bluemix_notm}}.

Nel seguente esempio per un file **js**, **3000** viene utilizzato come numero di porta. Utilizzando **3000**, puoi eseguire l'applicazione in locale per scopi di test e su {{site.data.keyword.Bluemix_notm}} senza apportare modifiche.

```
var port = (process.env.PORT || 3000);
```
{: codeblock}
