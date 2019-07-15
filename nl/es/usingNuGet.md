---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-31"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Acerca de la personalización de fuentes de paquetes de NuGet
{: #customizing_nuget}
Puede utilizar el archivo NuGet.Config en el directorio raíz de la aplicación para controlar dónde se descargan las dependencias de la aplicación. En el ejemplo siguiente, al configurar la propiedad `<packageSources>` se definen las claves y los URL de API para que la aplicación recupere paquetes.
```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
   <packageSources>
      <add key="NuGet.org" value="https://api.nuget.org/v3/index.json"/>
   </packageSources>
   </configuration>
```
{: codeblock}
