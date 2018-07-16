---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilice su propio JRE
{: #using_own_jre}

Puede ejecutar la aplicación Liberty en {{site.data.keyword.Bluemix}} con su propio JRE. Debe completar lo siguiente para que su JRE esté disponible en su aplicación.
* Alojar el JRE en una ubicación desde la que el paquete de compilación pueda descargarlo.
* Alojar un archivo `index.yml` que proporcione la ubicación del JRE.
* Configurar la aplicación para utilizar el JRE.

## Alojar el JRE e `index.yml`
{: #hosting_jre}

Debe alojar el archivo JRE en un servidor web desde el que el paquete de compilación pueda descargarlo. Puede alojar el archivo en {{site.data.keyword.Bluemix_notm}} con cualquiera de los servicios de servidor disponibles o puede alojarlo en una ubicación disponible públicamente. El servidor debe estar configurado con un archivo `index.yml` que especifique los detalles sobre el archivo JRE.

Complete los pasos siguientes para alojar el JRE y el archivo `index.yml`:
  1. Adquiera el JRE, que debe ser una versión que pueda utilizar en un SO UNIX de 64 bits, y debe ser un archivo `tar.gz`.
  2. Aloje el archivo JRE en una ubicación desde la que el paquete de compilación de Liberty pueda descargarlo.
  3. Proporcione un archivo `index.yml` en la ubicación de alojamiento. El archivo `index.yml` debe incluir una entrada que contenga un ID de versión del JRE seguido de una coma y el URL completo de dicho archivo JRE.
    * Define la versión del JRE en el archivo `index.yml`.

    ```
    ---
    jre_version: https://hostingLocation/jreName.tar.gz
    ```
    {: codeblock}

    * Incluya el ID de versión del JRE y complete la ubicación de archivo de JRE completa.  Por ejemplo:

    ```
    ---
    1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```
    {: codeblock}

## Configurar la app
{: #configure_app}

Debe establecer dos variables de entorno en la aplicación Liberty para configurar el paquete de compilación y que utilice un JRE alternativo. Establezca **JBP_CONFIG_OPENJDK** para que identifique la ubicación del archivo `index.yml` y establezca la variable de entorno **JVM** en *openjdk*. Para obtener más información sobre el formato de la versión de cadenas de valor de la versión, consulte la documentación de Cloud Foundry en [Sintaxis, ordenación y caracteres comodín de la versión ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/util-repositories.md){: new_window}.

El valor de la variable **JBP_CONFIG_OPENJDK** es la ubicación de archivo de `index.yml` y la versión JRE para elegir en el archivo index.yml.

```
'{repository_root: "https://locationToIndexYml", version: version-value}'
```
{: codeblock}

Emita el mandato `ibmcloud cf se myAPP` para establecer la variable **JBP_CONFIG_OPENJDK**, por ejemplo:
```
ibmcloud cf se myApp JBP_CONFIG_OPENJDK '{repository_root: "https://myHostingApp.ng.bluemix.net", version: 1.8.+}'
```
{: codeblock}

El URL *repository_root* no incluye `index.yml` en el URL. El URL *repository_root* apunta al nivel de directorio que contiene el archivo `index.yml`, no el propio archivo.

Para establecer la variable de entorno JVM, emita el mandato siguiente:
```
ibmcloud cf se myApp JVM 'openjdk'
```
{: codeblock}

**Nota**: Vuelva a transferir la aplicación después de establecer las variables de entorno para que los cambios entren en vigor.

## Confirmar
{: #confirmation}

Compruebe el registro de transición para confirmar que Liberty está utilizando el JRE esperado. Busque el mensaje que indica que el servidor ha descargado el paquete de compilación de la ubicación indicada en el archivo `index.yml`. Consulte el siguiente fragmento de código para obtener un ejemplo de la salida de registro cuando Liberty utilice correctamente el JRE esperado.
```
 -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}
