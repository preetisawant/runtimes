---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Limites de memória e o buildpack do Liberty
{: #memory_limits}

Um limite de memória deve ser especificado ao implementar um aplicativo com o buildpack do Liberty.

## Limites de memória e o buildpack do Liberty
{: #memory_limits_and_liberty}


Ao implementar um aplicativo com o
buildpack do Liberty, um "Limite de memória" será solicitado a você. O buildpack do Liberty for Java define uma razão de tamanho de memória heap padrão para evitar que seu processo exceda o limite de memória. Também é possível especificar o tamanho ou razão de memória heap definindo as variáveis ambientais `JVM_ARGS` ou `JBP_CONFIG_IBMJDK`. Veja [Opções de memória heap](#heap_memory_options) para saber mais.

Para determinar qual Limite de memória especificar,
é importante entender que você não está especificando o tamanho do heap de aplicativo Java. Você está especificando a quantia de memória disponível para o contêiner do Diego ou o DEA a ser usado. Esta quantia inclui a memória
que é usada pelos componentes a seguir:

* pelo contêiner warden.
* para mapear as extensões kernel e bibliotecas do sistema para o processo.
* para executáveis jvm, heap de trabalho jvm, espaço jit e referências compactadas.
* para classes (servidor de aplicativos e aplicativo), pilhas de encadeamento e buffers de E/S diretos.
* pelo heap do aplicativo Java.

Mais informações sobre o uso de memória JVM podem ser localizadas no artigo do developerWorks [Obrigado pela memória](http://www.ibm.com/developerworks/library/j-nativememory-linux/)

Ao implementar
um aplicativo, o uso de memória do processo inteiro é monitorado. Se o uso de memória exceder o limite de memória
que você especificou quando o aplicativo foi implementado, o kernel irá parar o processo. Esta ação acontece sem aviso e pode ser manifestada de várias maneiras.

 Se o Limite de memória for excedido durante a implementação do aplicativo, você receberá uma mensagem de que ocorreu uma falha e poderá ver qualquer um dos seguintes.

  * Talvez
veja que o aplicativo está oscilando.
  * Você pode ver que o aplicativo tentou ser iniciado várias vezes, sempre sem êxito.
  * Você pode receber uma mensagem indicando que a implementação do aplicativo falhou.

Se o Limite de memória for excedido enquanto o aplicativo estiver em serviço, o processo parará e o Cloud Foundry tentará reiniciar o aplicativo. É possível que o aplicativo seja reiniciado, mas ficará indisponível por algum tempo.

## Opções de memória heap
{: #heap_memory_options}

É possível customizar de várias maneiras a quantia máxima de memória heap alocada a seu aplicativo, por exemplo, com o uso da
variável de ambiente `JVM_ARGS`, com a mudança do arquivo `jvm.options` ou com a configuração da variável de ambiente `JBP_CONFIG_IBMJDK`, que controla o `heap_size_ratio`. Se você não especificar quaisquer configurações, o buildpack usará as configurações padrão.

### Padrões de memória heap
{: .#heap_memory_defaults}
Para evitar erros que resultam de exceder os limites de memória, o buildpack do Liberty for Java configura uma razão de tamanho de heap padrão dependendo do limite de memória que você especifica quando implementa seu aplicativo.

* Aplicativos com limites de memória menores que 512 M têm uma razão de tamanho de heap de 50%
* Aplicativos que têm limites de memória maiores ou iguais a 512 M têm uma razão de tamanho de heap de 75%

Ao especificar a memória heap usando variáveis de ambiente, você substitui as razões de tamanho de heap padrão.

### Especificando memória heap
{: #specifying_heap_memory}

É possível configurar o tamanho de memória heap usando variáveis de ambiente ou mudando o arquivo `jvm.options`. Ao usar as variáveis de ambiente `JVM_ARGS` ou `JBP_CONFIG_IBMJDK`, quaisquer mudanças entrarão em
vigor quando enviar seu aplicativo por push para {{site.data.keyword.Bluemix_notm}}. Mudando o arquivo `jvm.options`, o efeito para a configuração de tamanho de heap também pode ser testado localmente.

* Use a variável de ambiente `JVM_ARGS` e o argumento -Xmx. Por exemplo, para configurar o tamanho máximo de heap como 512 M,
use o comando a seguir e, em seguida, remonte seu app.

```
    ibmcloud cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* Especifique a razão de tamanho de heap usando a variável de ambiente JBP_CONFIG_IBMJDK.  O heap_size_ratio é um valor de vírgula flutuante que especifica a quantidade de limite de memória para alocar para o heap.  Por exemplo, para alocar metade da memória disponível para o heap (50% ou 0,50), emita o comando a seguir e remonte seu app.

```
    ibmcloud cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}

* Especifique o argumento -Xmx no arquivo jvm.options se seu aplicativo for um [diretório do servidor](/docs/runtimes/liberty/optionsForPushing.html#server_directory) ou um [servidor em pacote](/docs/runtimes/liberty/optionsForPushing.html#packaged_server). Para obter mais informações sobre o uso do arquivo `jvm.options` com o tempo de execução do Liberty, veja [Configurando uma JVM genérica](http://www-01.ibm.com/support/docview.wss?uid=swg21596474).  
