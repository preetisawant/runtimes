---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Acerca de bibliotecas personalizadas
{: #use_customlib}

{: #shortdesc}

## Utilización de bibliotecas nativas personalizadas
{: #using_custom_native_libraries}

Algunas bibliotecas pueden requerir que utilice un paquete NuGet y algunos archivos de bibliotecas nativas ( archivos .so).  Para utilizar estas bibliotecas con el paquete de compilación, debe colocarlas en una carpeta denominada *ld_library_path* en la carpeta raíz de la aplicación.
El paquete de compilación añadirá automáticamente esta vía de acceso a la variable de entorno `LD_LIBRARY_PATH` durante la transferencia.  Como alternativa, puede especificar la variable de entorno `LD_LIBRARY_PATH` en el archivo `manifest.yml` de la aplicación o mediante el mandato `ibmcloud cf set-env` para que utilice un nombre de carpeta que no sea *ld_library_path*.  En este caso, el paquete de compilación añadirá esta vía de acceso personalizada a la variable `LD_LIBRARY_PATH` generada por el paquete de compilación.
