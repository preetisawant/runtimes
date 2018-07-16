---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Informazioni sulle librerie personalizzate
{: #use_customlib}

{: #shortdesc}

## Utilizzo delle librerie native personalizzate.
{: #using_custom_native_libraries}

Alcune librerie possono richiederti di utilizzare sia un pacchetto NuGet che alcuni file della libraria nativa (file .so).  Per poter utilizzare queste librerie con il pacchetto di build, dovresti posizionarle in una cartella denominata *ld_library_path* nella cartella root della tua applicazione.
Il pacchetto di build aggiungerà automaticamente questo percorso alla variabile di ambiente `LD_LIBRARY_PATH` durante la fase di preparazione.  In alternativa, puoi specificare la variabile di ambiente `LD_LIBRARY_PATH` nel file `manifest.yml` della tua applicazione o utilizzando il comando `ibmcloud cf set-env` per utilizzare un nome della cartella differente da *ld_library_path*.  In questo caso, il pacchetto di build accoderà questo percorso personalizzato alla variabile `LD_LIBRARY_PATH` generata dal pacchetto di build.
