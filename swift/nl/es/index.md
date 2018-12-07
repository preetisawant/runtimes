---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Cloud Runtime for Swift
{: #swift_runtime}

Runtime for Swift en {{site.data.keyword.Bluemix}} está basado en el paquete de compilación de [{{site.data.keyword.Bluemix_notm}} for Swift](https://github.com/IBM-Swift/swift-buildpack) (es decir, swift_buildpack).
El paquete de compilación proporciona un entorno de ejecución completo para aplicaciones Swift.
{: shortdesc}

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix_notm}} proporciona una aplicación de inicio basada en [Kitura ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Cloud/Kitura-Starter). La app de inicio de Kitura es una app de Swift sencilla que puede utilizar para obtener más información sobre los tipos de aplicaciones de servidor que puede desarrollar utilizando el lenguaje de programación Swift. Esta app de ejemplo crea un servidor HTTP Kitura básico que devuelve el contenido HTML al cliente.

**Nota:** la app de inicio de Kitura está pensada para utilizarse para fines educativos. Puede experimentar con la app de inicio realizando mejoras y enviar por push dichos cambios al entorno de {{site.data.keyword.Bluemix_notm}}. Consulte [Utilización de las aplicaciones de inicio](../common/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Cambiar el nombre de la app
{: #renaming_your_app}

Si desea cambiar el nombre de la app, desde el iniciador de Kitura, o en general, es necesario llevar a cabo unos pocos cambios. Esto evitará confusión y garantizará un despliegue sin errores.

- Cambie el nombre de la carpeta de proyecto de la app para que coincida con el nombre de su app.
- `Package.swift`: cambie las siguientes entradas:
    - `name`: debe coincidir con el nombre de la app.
    - `targets[Target(name:)]`: debe coincidir con el nombre de la app.
- `manifest.yml`: cambie las siguientes entradas:
    - `name`: debe coincidir con el nombre de la app.
    - `command`: el nombre del ejecutable para iniciar la app (debe coincidir con el nombre especificado en el archivo Package.swift).

## Versiones de tiempo de ejecución
{: #runtime_versions}

[Runtime for Swift ![Icono a enlace externo](../../icons/launch-glyph.svg "Icono a enlace externo")](https://github.com/IBM-Swift/swift-buildpack) (swift_buildpack) alojado en {{site.data.keyword.Bluemix_notm}} está actualizado para utilizar la última versión de GA en los binarios de Swift. Esta es la versión recomendada de Swift para utilizar en su app. El paquete de compilación no enumera otras versiones de Swift en sus archivos [manifest.yml ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml), que se guardan en la memoria caché en el paquete de compilación para proporcionar un tiempo de suministro reducido.

Si desea utilizar una versión distinta de Swift en {{site.data.keyword.Bluemix_notm}} para la aplicación, puede especificar la versión con un archivo `.swift-version` en la raíz del repositorio. Este archivo `.swift-version` define qué versión de Swift va a utilizar swift_buildpack.

```
$ cat .swift-version
4.1.2
```
{: pre}

Puesto que hay frecuentes actualizaciones en el idioma de Swift, siempre debe incluir un archivo `.swift-version` para que la app se "ancle" a la versión de Swift con la que normalmente funciona la aplicación.

Tenga en cuenta que puede especificar cualquier versión válida de Swift en el archivo `.swift-version`. Estas versiones alteradas deben coincidir con la denominación de [Swift.org ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://swift.org/download/), desde donde se descargan directamente. Aunque al utilizar una versión no almacenada en memoria caché se tardará más en el suministro, no hay diferencia de rendimiento del tiempo de ejecución de la app Swift.

Se utiliza el swift_buildpack predeterminado en {{site.data.keyword.Bluemix_notm}} si el directorio raíz de la app contiene un archivo `Package.swift`.  Si desea utilizar un paquete de compilación alternativo, debe especificarlo añadiendo una entrada `buildpack: {buildpackUrl}` en el archivo manifest.yml de la app. De forma alternativa, puede definirlo en el momento del despliegue utilizando el argumento de mandatos `ibmcloud cf push -b {buildpackUrl}`.


## Entornos de desarrollador

Los desarrolladores tienen varias opciones al crear aplicaciones del lado del servidor con Swift. Aquellos que utilicen dispositivos macOS de Apple podrían preferir utilizar Xcode IDE, aunque no es un requisito.  Las apps basadas en Swift que se desplegarán y ejecutarán en {{site.data.keyword.Bluemix_notm}} pueden utilizar cualquier editor de programación o IDE.  El realce y la comprobación de la sintaxis para Swift está disponible para muchos editores populares. La herramienta de línea de mandatos REPL de Swift que se incluye en los binarios desde [Swift.org![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://swift.org/), permite una compilación y comprobación local antes de desplegar en {{site.data.keyword.Bluemix_notm}}.

Los usuarios de macOS pueden utilizar la [Kitura App ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.kitura.io/app.html) que simplifica la creación, el desarrollo, la gestión y el control de apps Swift del lado del servidor que se ejecutan en {{site.data.keyword.Bluemix_notm}}.  


## Integración mejorada

Trabajar con la [infraestructura web de Kitura](http://ibm-swift.github.io/Kitura/) proporciona muchas prestaciones. Kitura es modular por naturaleza y pronto verá ampliada su funcionalidad con SDK empaquetados, para proporcionar características tales como la autenticación, el acceso a servicios basados en Watson y una amplia variedad de bases de datos.  Kitura proporciona soporte para muchas bases de datos directamente, aunque otros proyectos de código abierto también proporcionan SDK para muchas plataformas de base de datos. A continuación encontrará una lista no exhaustiva de los SDK proporcionados por Kitura para trabajar con recursos externos.

- [IBM Watson Developer Cloud Swift SDK ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/watson-developer-cloud/swift-sdk/)
- [SwiftMetrics ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/RuntimeTools/SwiftMetrics)
- [IBM Cloudant y CouchDB ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Swift/Kitura-CouchDB)
- [KituraKit ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Swift/KituraKit)
- [Swift Kuery ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Swift/Swift-Kuery/)
- [Swift Kuery ORM ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Swift/Swift-Kuery-ORM)

Para encontrar más paquetes Swift para incluir en la aplicación, vaya a la sección de paquetes de [Kitura.io](https://www.kitura.io/packages.html). Los paquetes pueden añadirse a una aplicación Swift incluyendo los detalles de versión y el URL de Git del paquete en el archivo `Package.swift` de la app. Para obtener más detalles sobre la gestión de paquetes, consulte la [sección de Package Manager de Swift.org](https://swift.org/package-manager/).


## Información relacionada

También hay otras herramientas en línea disponibles en IBM para el desarrollador de Swift.
- [IBM Swift DevCenter ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/swift/) - Sitio de destino principal para toda la información de IBM. Puede encontrar información sobre nuestras ofertas, blogs, eventos sociales, documentación y más.
- [Kitura.io ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.kitura.io/index.html) proporciona noticias, ejemplos y recursos para crear aplicaciones Kitura.
- [Swift@IBM Slack ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://swift-at-ibm-slack.mybluemix.net/) proporciona foros para plantear dudas y resolver problemas con el equipo de Swift@IBM.
