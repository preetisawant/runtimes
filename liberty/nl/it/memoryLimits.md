---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-14"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Limiti di memoria e pacchetto di build Liberty
{: #memory_limits}

Quando distribuisci un'applicazione con il pacchetto di build Liberty, è necessario specificare
un limite di memoria.

## Limiti di memoria e pacchetto di build Liberty
{: #memory_limits_and_liberty}


Quando
distribuisci un'applicazione con il pacchetto di build Liberty, ti viene richiesto
un "Limite di memoria". Il pacchetto di build Liberty for Java configura un rapporto della dimensione della memoria di heap per evitare che il tuo processo superi il limite di memoria. Puoi anche specificare il rapporto o la dimensione della memoria di heap definendo le variabili di ambiente `JVM_ARGS` o `JBP_CONFIG_IBMJDK`. Consulta [Opzioni memoria di heap](#heap_memory_options) per ulteriori informazioni.

Per determinare quale limite di memoria specificare, è
importante comprendere che non stai specificando la dimensione dell'heap delle applicazioni
Java. Stai specificando la quantità di memoria disponibile per il contenitore Diego o DEA da utilizzare. Questa quantità include la memoria utilizzata dai seguenti componenti:

* dal contenitore Warden. 
* per associare le estensioni kernel e le librerie di sistema nel processo. 
* per gli eseguibili jvm, l'heap di lavoro jvm, lo spazio jit e i riferimenti compressi. 
* per le classi (server delle applicazioni e applicazione), gli stack di thread e i buffer di I/O diretto. 
* dall'heap delle applicazioni Java. 

Ulteriori informazioni sull'utilizzo della memoria JVM sono disponibili nell'articolo developerWorks [Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/)

Quando distribuisci un'applicazione, viene monitorato l'utilizzo della memoria dell'intero processo. Se l'utilizzo della memoria supera il limite di memoria da te specificato quando è stata distribuita l'applicazione, il kernel arresta il processo. Questa azione si verifica senza alcuna avvertenza e potrebbe manifestarsi in diversi modi. 

 Se il limite di memoria viene superato durante la distribuzione dell'applicazione, ricevi un messaggio che segnala
che si è verificato un errore e potresti visualizzare quanto segue. 

  * Potresti notare che l'applicazione è instabile.
  * Potresti vedere che l'applicazione ha provato l'avvio più volte, sempre con esito negativo.
  * Potresti ricevere un messaggio che indica che la distribuzione dell'applicazione non è riuscita. 

Se il limite di memoria viene superato mentre l'applicazione è in funzione, il processo viene arrestato e Cloud Foundry tenta di riavviare l'applicazione. È possibile che l'applicazione venga riavviata, ma non sarà disponibile per un certo lasso di tempo.

## Opzioni memoria di heap
{: #heap_memory_options}

Puoi personalizzare la quantità massima di memoria heap assegnata alla tua applicazione in vari modi utilizzando la variabile di ambiente `JVM_ARGS`, modificando il file `jvm.options` o configurando la variabile di ambiente `JBP_CONFIG_IBMJDK` che controlla `heap_size_ratio`. Se non specifichi alcuna impostazione, il pacchetto di build utilizza l'impostazione predefinita.

### Valori predefiniti della memoria di heap 
{: .#heap_memory_defaults}
Per evitare errori riguardanti il superamento dei limiti di memoria, il pacchetto di build Liberty for Java configura un rapporto di dimensione di heap predefinito nel limite di memoria che specifichi quando distribuisci la tua applicazione.

* Le applicazioni con limiti di memoria inferiori a 512M hanno un rapporto di dimensione di heap del 50%
* Le applicazioni con limiti di memoria maggiori o uguali a 512M hanno un rapporto di dimensione di heap del 75%

Quando specifichi la memoria di heap che utilizza le variabili di ambiente, sovrascrivi i rapporti di dimensione di heap predefiniti.

### Specifica della memoria heap
{: #specifying_heap_memory}

Puoi impostare la dimensione della memoria di heap utilizzando le variabili di ambiente o modificando il file `jvm.options`. Quando utilizzi le variabili di ambiente `JVM_ARGS` o `JBP_CONFIG_IBMJDK`, tutte le modifiche avranno effetto dopo aver trasmesso la tua applicazione a Bluemix. Modificando il file `jvm.options`, l'effetto della configurazione della dimensione di heap può venire verificato anche localmente.

* Utilizza la variabile di ambiente `JVM_ARGS` e l'argomento -Xmx. Ad esempio per impostare la dimensione heap massima di 512M
utilizza il seguente comando, quindi riprepara la tua applicazione.

```
    $ cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* Specifica il rapporto della dimensione heap utilizzando la variabile di ambiente JBP_CONFIG_IBMJDK. heap_size_ratio è un
valore a punto mobile che specifica quale limite di memoria assegnare all'heap. Ad esempio, per assegnare
metà della memoria disponibile all'heap (50% o 0.50), immetti il seguente comando e riprepara la tua applicazione.

```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}

* Specifica l'argomento -Xmx nel file jvm.options se la tua applicazione è una [directory server](optionsForPushing.html#server_directory) o un [server in pacchetto](optionsForPushing.html#packaged_server). Per ulteriori informazioni sull'utilizzo del file `jvm.options` con il runtime Liberty, consulta [Setting generic JVM](http://www-01.ibm.com/support/docview.wss?uid=swg21596474).  
