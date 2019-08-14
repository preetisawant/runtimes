---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Límites de memoria y el paquete de compilación de Liberty
{: #memory_limits}

Se debe especificar un límite de memoria cuando se despliega una aplicación con el paquete de compilación de Liberty.

## Límites de memoria y el paquete de compilación de Liberty
{: #memory_limits_and_liberty}


Cuando despliegue una aplicación con el paquete de compilación de Liberty, se le solicitará un "Límite de memoria". El paquete de compilación de Liberty for Java establece una proporción de tamaño de memoria de almacenamiento dinámico predeterminada para evitar que el proceso supere el límite de memoria. También puede especificar la proporción o el tamaño de memoria de almacenamiento dinámico definiendo las variables de entorno `JVM_ARGS` o `JBP_CONFIG_IBMJDK`. Consulte [Opciones de memoria de almacenamiento dinámico](#heap_memory_options) para obtener más información.

Para determinar el límite de memoria que debe especificar, es importante comprender que no está especificando el tamaño del almacenamiento dinámico de la aplicación Java. Está especificando la cantidad de memoria disponible que puede utilizar el DEA o el contenedor de Diego. Esta cantidad incluye la memoria que utilizan los siguientes componentes:

* El contenedor Warden.
* Para correlacionar extensiones del kernel y bibliotecas del sistema en el proceso.
* Para los ejecutables jvm, el almacenamiento dinámico de trabajo de jvm, el espacio de jit y las referencias comprimidas.
* Para las clases (servidor de aplicaciones y aplicación), las pilas de hebras y los almacenamientos intermedios de E/S directa.
* El almacenamiento dinámico de la aplicación Java.

Encontrará más información sobre el uso de memoria de JVM en el artículo de developerWorks [Gracias por la memoria](http://www.ibm.com/developerworks/library/j-nativememory-linux/)

Cuando despliega una aplicación, se supervisa el uso de memoria de todo el proceso. Si el uso de memoria supera el límite de la memoria que ha especificado al desplegar la aplicación, el kernel detiene el proceso. Esta acción sucede sin aviso y se puede manifestar de varias formas.

 Si el límite memoria se excede durante el despliegue de la aplicación, recibirá un mensaje que indica que se ha producido un error y puede ocurrir una de las situaciones siguientes.

  * Es posible que vea que la aplicación se comporta de forma inestable.
  * Puede que vea que la aplicación ha intentado iniciarse varias veces, siempre sin éxito.
  * Es posible que reciba un mensaje que indique que la aplicación no se ha podido desplegar.

Si el límite memoria se excede mientras la aplicación está en funcionamiento, el proceso se detiene y Cloud Foundry intenta reiniciar la aplicación. Es posible que la aplicación se reinicie, pero no estará disponible durante algún tiempo.

## Opciones de memoria de almacenamiento dinámico
{: #heap_memory_options}

Puede personalizar la cantidad máxima de memoria de almacenamiento dinámico que tiene asignada la aplicación de varias formas, como utilizando la variable de entorno `JVM_ARGS`, modificando el archivo `jvm.options` o definiendo la variable de entorno `JBP_CONFIG_IBMJDK` que controla el valor `heap_size_ratio`. Si no especifica ningún valor, el paquete de compilación utiliza los valores predeterminados.

### Valores predeterminados de memoria de almacenamiento dinámico
{: .#heap_memory_defaults}
Para evitar errores provocados por superar los límites de memoria, el paquete de compilación de Liberty for Java establece una proporción predeterminada de tamaño de almacenamiento dinámico que depende del límite de memoria que especifique al desplegar la aplicación.

* Las aplicaciones con límites de memoria inferiores a 512 M tienen una proporción de tamaño de almacenamiento dinámico del 50%
* Las aplicaciones con límites de memoria superiores o iguales a 512 M tienen una proporción de tamaño de almacenamiento dinámico del 75%

Cuando especifica la memoria de almacenamiento dinámico utilizando variables de entorno, se sustituyen las proporciones predeterminadas de tamaño de almacenamiento dinámico.

### Especificación de la memoria de almacenamiento dinámico
{: #specifying_heap_memory}

Puede establecer el tamaño de la memoria de almacenamiento dinámico utilizando variables de entorno o cambiando el archivo `jvm.options`. Si utiliza las variables de entorno `JVM_ARGS` o `JBP_CONFIG_IBMJDK`, los cambios entrarán en vigor cuando envíe por push la aplicación a {{site.data.keyword.Bluemix_notm}}. Al cambiar el archivo `jvm.options`, el efecto en la configuración del tamaño de almacenamiento dinámico también se puede probar localmente.

* Utilice la variable de entorno `JVM_ARGS` y el argumento -Xmx. Por ejemplo, para establecer el tamaño máximo de memoria de almacenamiento dinámico en 512 M utilice el mandato siguiente y luego vuelva a transferir la app.

```
    ibmcloud cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* Especifique la proporción del tamaño de almacenamiento dinámico utilizando la variable de entorno JBP_CONFIG_IBMJDK.  La proporción heap_size_ratio es un valor de coma flotante que especifica la cantidad de límite de memoria que se asignará al almacenamiento dinámico.  Por ejemplo, para asignar la mitad de la memoria disponible al almacenamiento dinámico (50% o 0,50), emita el mandato siguiente y vuelva a transferir la app.

```
    ibmcloud cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}

* Especifique el argumento -Xmx en el archivo jvm.options si la aplicación es un [directorio de servidor](/docs/runtimes/liberty/optionsForPushing.html#server_directory) o un [servidor empaquetado](/docs/runtimes/liberty/optionsForPushing.html#packaged_server). Para obtener más información sobre el uso del archivo `jvm.options` con archivo con el tiempo de ejecución de Liberty, consulte [Establecer argumentos JVM genéricos](http://www-01.ibm.com/support/docview.wss?uid=swg21596474).  
