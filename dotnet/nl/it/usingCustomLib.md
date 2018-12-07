---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Utilizza le librerie native personalizzate
{: #use_customlib}

Alcune librerie potrebbero richiedere che utilizzi sia un pacchetto NuGet che alcuni file della libreria nativa (file `.so`).  

Per utilizzare queste librerie con il pacchetto di build, inseriscile in una cartella `ld_library_path` all'interno della cartella root della tua applicazione. Il pacchetto di build aggiunge automaticamente questo percorso alla variabile di ambiente `LD_LIBRARY_PATH` durante la fase di preparazione.  

In alternativa, puoi specificare la variabile di ambiente `LD_LIBRARY_PATH` nel file `manifest.yml` della tua applicazione o utilizzando il comando `ibmcloud cf set-env` per utilizzare un nome cartella diverso da `ld_library_path`.  In questo caso, il pacchetto di build accoda questo percorso personalizzato al `LD_LIBRARY_PATH` generato dal pacchetto di build.
