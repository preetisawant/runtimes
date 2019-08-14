---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-26"
subcollection: "Nodejs"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Ejecutar la aplicación Node.js localmente
{: #hints}

Establezca un número de puerto para ejecutar la aplicación Node.js localmente sin causar conflictos al ejecutarla en {{site.data.keyword.Bluemix}}.
{: shortdesc}

Cuando la aplicación se ejecuta en {{site.data.keyword.Bluemix_notm}}, Cloud Foundry asigna la variable de entorno PORT. Sin embargo, cuando la aplicación se ejecuta localmente, PORT no está definido, de modo que no puede definir el puerto para la aplicación. Para evitar conflictos, defina el puerto en el que la app está a la escucha localmente algo distinto al puerto utilizado por {{site.data.keyword.Bluemix_notm}}.

En el ejemplo siguiente para un archivo **js**, **3000** se utiliza como el número de puerto. Utilizando **3000**, puede ejecutar la aplicación localmente para realizar pruebas y en {{site.data.keyword.Bluemix_notm}} sin realizar cambios.

```
var port = (process.env.PORT || 3000);
```
{: codeblock}
