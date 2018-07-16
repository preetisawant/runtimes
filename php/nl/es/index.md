---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}

El tiempo de ejecución de PHP en {{site.data.keyword.Bluemix}} está basado en el php_buildpack.
El php_buildpack proporciona un entorno de ejecución completo para apps PHP.
{: shortdesc}

El php_buildpack se utiliza en las condiciones siguientes:
* Su app contiene un archivo composer.json, o
* su app contiene un archivo *.php, o
* su app define una variable ${WEBDIR} en su archivo [options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html), y dicha variable se establece en un directorio existente dentro de su app.

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una app de inicio de PHP.  La aplicación de inicio de PHP es una app de PHP simple que proporciona una plantilla que puede utilizar para la app. Puede experimentar con la app de iniciador, y realizar y enviar por push cambios en el entorno de {{site.data.keyword.Bluemix}}.  Consulte [Utilización de las aplicaciones de inicio](../common/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Aplicar HTTPS en todas las páginas de la aplicación
{: #enforce_https}

Para aplicar el uso de HTTPS en lugar de HTTP en todas las páginas de la aplicación cuando se ejecuta en {{site.data.keyword.Bluemix_notm}} utilizando Apache, es necesario realizar los cambios siguientes en el archivo ".htaccess".  Esta regla se aplicará a cualquier solicitud que no se haya hecho mediante HTTPS solo cuando se ejecute en {{site.data.keyword.Bluemix_notm}}.

```
RewriteCond %{HTTP:X-Forwarded-Proto} !=https [NC]
RewriteCond %{ENV:BLUEMIX_REGION} !^$
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede especificar la versión de PHP que utilizará la app en el archivo composer.json. Por ejemplo:

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
Para obtener más información, consulte [enlaces de Composer Package ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://getcomposer.org/doc/04-schema.md#package-links).

Cuando no se especifique una versión, se elegirá la versión 5.6.31 de forma predeterminada.

### Versiones disponibles:
{: #available_versions}

Las siguientes versiones de PHP están disponibles en el
[paquete de compilación de PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.27)
actualmente instalado en {{site.data.keyword.Bluemix}}:

* 5.6.30
* 5.6.31
* 7.0.20
* 7.0.21
* 7.1.6
* 7.1.7

Si la app requiere una versión de PHP que no aparece en la lista,
puede utilizar el
[paquete de compilación de PHP](https://github.com/cloudfoundry/php-buildpack.git) externo para
desplegar la app.
