---

copyright:
  years: 2018
lastupdated: "2018-12-14"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:tip: .tip}

# Instalar características de Liberty
{: #install-features}

El entorno de tiempo de ejecución de Liberty for Java incluye [un subconjunto de características](libertyFeatures.html#liberty_features) que están disponibles en Liberty. Puede instalar características que no están incluidas en el entorno de tiempo de ejecución ejecutando el mandato `installUtility` de Liberty como hook previo al tiempo de ejecución de Cloud Foundry cuando la aplicación se envía a {{site.data.keyword.cloud_notm}}.

Para ver una lista completa de las características disponibles, consulte [Características de Liberty ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html).

Para obtener información sobre cómo utilizar los hooks previos al tiempo de ejecución, consulte [Configurar hooks previos al tiempo de ejecución ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.cloudfoundry.org/devguide/deploy-apps/deploy-app.html#profile) en la documentación de Cloud Foundry.

1. En el directorio raíz de la aplicación que desea enviar por push a {{site.data.keyword.cloud_notm}}, cree un directorio `.profile.d`.

1. En el directorio `.profile.d`, cree un archivo de script que ejecute el mandato `installUtility` tal como se muestra en el ejemplo siguiente.

   Este ejemplo instala la característica `audit-1.0`.

   ```
   #!/bin/sh
   echo "Instalando audit-1.0"
   export PATH=$PATH:$HOME/.java/jre/bin

   $HOME/.liberty/bin/installUtility install audit-1.0 --acceptLicense
   ```
   {: codeblock}

   Puede instalar varias características especificando los nombres de las características adicionales separados por espacios.
   {: tip}

1. Envíe por push la app a {{site.data.keyword.cloud_notm}}, utilizando el parámetro `-p` para especificar el directorio raíz de la aplicación.

   Por ejemplo, ejecute el siguiente mandato para enviar por push la app:
   ```
   ibmcloud cf push myApp -p /<path-to-application>
   ```
   {: codeblock}

1. Verifique que la característica se ha instalado correctamente visualizando el registro reciente de la aplicación.

   Por ejemplo, ejecute el mandato siguiente para visualizar el registro:
   ```
   ibmcloud cf logs myApp --recent
   ```
   {: codeblock}

    Si la característica se ha instalado, la salida muestra los siguientes mensajes:

    ```
    2018-09-18T13:01:17.61-0400 [APP/PROC/WEB/0] OUT Instalando audit-1.0
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT Estableciendo una conexión con los repositorios configurados...
    2018-09-18T13:01:19.13-0400 [APP/PROC/WEB/0] OUT Este proceso podría tardar varios minutos en completarse.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Se ha conectado correctamente con todos los repositorios configurados.
    2018-09-18T13:01:21.28-0400 [APP/PROC/WEB/0] OUT Preparando activos para la instalación. Este proceso podría tardar varios minutos en completarse.
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT Se ha encontrado el argumento --acceptLicense. Esto indica que ha
    2018-09-18T13:01:25.87-0400 [APP/PROC/WEB/0] OUT aceptado las condiciones del acuerdo de licencia.
    ```
