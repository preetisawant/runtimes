---

copyright:
  years: 2017
lastupdated: "2017-12-15"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Resolución de problemas de SDK for Node.js
{: #ts}


Aquí encontrará las respuestas a preguntas frecuentes sobre la resolución de problemas sobre el uso de SDK for Node.js en {{site.data.keyword.Bluemix}}.
{:shortdesc}

Para obtener más información sobre el registro y el rastreo, consulte la sección [Rastreo](../../manageapps/app_mng.html#trace) de [Gestión de aplicaciones de Liberty y Node.js](../../manageapps/app_mng.html).

## La aplicación no se inicia con el error “No queda espacio en el dispositivo”
{: #no_space_left_on_device}


Una aplicación Node.js no se inicia con el error “No queda espacio en el dispositivo”. Por ejemplo, el error puede parecerse al siguiente en los registros:
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: No se puede grabar: No queda espacio en el dispositivo

```
{: #codeblock}

Las aplicaciones Node.js que utilizan versiones de NPM anteriores a la versión 3 consumen más espacio al descargar dependencias.
{: tsCauses}

Modifique el archivo package.json de la aplicación de modo que utilice NPM versión 3 o posterior.
{: tsResolve}

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}

## La aplicación se reinicia debido a restricciones de memoria
{: #oom}

Node.js no sabe cuánta memoria está disponible para la aplicación, de modo que el recopilador de basura no puede ejecutarse antes de que se agote la memoria.

```
2017-09-01T11:00:42.19-0400 [APP/PROC/WEB/0]OUT Exit status 137
2017-09-01T11:00:42.23-0400 [CELL/0]     OUT Exit status 0
2017-09-01T11:00:42.27-0400 [CELL/0]     OUT Destroying container
2017-09-01T11:00:42.34-0400 [API/0]      OUT Process has crashed with type: "web"
2017-09-01T11:00:42.36-0400 [API/0]      OUT App instance exited with guid eecfba3b-430c-4a6b-b71f-ac72816fe152 payload: {"instance"=>"77dbb981-16d0-3a05-3235-9a4b", "index"=>0, "reason"=>"CRASHED", "exit_description"=>"2 error(s) occurred:\n\n* 2 error(s) occurred:\n\n* Exited with status 137 (out of memory)\n* cancelled\n* cancelled", "crash_count"=>1, "crash_timestamp"=>1504278042244633291, "version"=>"6497b5b5-67d4-4c5a-b1af-362e522a029d"}
2017-09-01T11:00:43.35-0400 [CELL/0]     OUT Successfully destroyed container
```
{: codeblock}

Una posible solución es establecer la opción `--max_old_space_size` en el mandato de inicio de la aplicación en el archivo package.json. Esta opción representa parte de la ocupación de memoria de la aplicación y debe establecerse en un valor inferior a la memoria total disponible para la aplicación. Más información sobre [Grandes picos de memoria y Heroku](https://github.com/nodejs/node/issues/3370) para un debate más profundo de este tema.
```
  "scripts": {
    "start": "node --max_old_space_size=800 server.js"
  }
```
{: codeblock}
