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

# Resolução de problemas do SDK for Node.js
{: #ts}


Aqui estão as respostas para as perguntas comuns de resolução de problemas sobre o uso do SDK for Node.js no {{site.data.keyword.Bluemix}}.
{:shortdesc}

Para saber mais sobre criação de log e rastreio, consulte a seção
[Rastreio](../../manageapps/app_mng.html#trace) em [Gerenciando os
aplicativos Liberty e Node.js](../../manageapps/app_mng.html).

## O aplicativo falha ao ser iniciado com um erro "Não sobrou nenhum espaço no dispositivo"
{: #no_space_left_on_device}


Um aplicativo Node.js falha ao iniciar com um erro "Não sobrou nenhum espaço no dispositivo". Por exemplo, o
erro nos logs pode ser semelhante ao seguinte:
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

Os aplicativos Node.js que usam versões do NPM anteriores à versão 3 consomem mais espaço ao fazer download de dependências.
{: tsCauses}

Modifique o arquivo package.json de seu aplicativo para usar uma versão NPM 3 ou superior.
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

## Reinicializações do aplicativo devido a restrições de memória
{: #oom}

O Node.js não sabe quanta memória está disponível para o aplicativo, portanto o coletor de lixo pode não ser executado antes de a memória estar esgotada.

```
2017-09-01T11:00:42.19-0400 [APP/PROC/WEB/0]OUT Exit status 137
2017-09-01T11:00:42.23-0400 [CELL/0]     OUT Exit status 0
2017-09-01T11:00:42.27-0400 [CELL/0]     OUT Destroying container
2017-09-01T11:00:42.34-0400 [API/0]      OUT Process has crashed with type: "web"
2017-09-01T11:00:42.36-0400 [API/0]      OUT App instance exited with guid eecfba3b-430c-4a6b-b71f-ac72816fe152 payload: {"instance"=>"77dbb981-16d0-3a05-3235-9a4b", "index"=>0, "reason"=>"CRASHED", "exit_description"=>"2 error(s) occurred:\n\n* 2 error(s) occurred:\n\n* Exited with status 137 (out of memory)\n* cancelled\n* cancelled", "crash_count"=>1, "crash_timestamp"=>1504278042244633291, "version"=>"6497b5b5-67d4-4c5a-b1af-362e522a029d"}
2017-09-01T11:00:43.35-0400 [CELL/0]     OUT Successfully destroyed container
```
{: codeblock}

Uma solução possível é configurar a opção `--max_old_space_size` no comando inicial do aplicativo no arquivo package.json. Essa opção representa parte da área de cobertura da memória do aplicativo e deve ser configurada para um valor menor que a memória total disponível para o aplicativo. Leia sobre [Aumentos grandes de memória e Heroku](https://github.com/nodejs/node/issues/3370) para uma discussão mais detalhada deste tópico.
```
  "scripts": {
    "start": "node --max_old_space_size=800 server.js"
  }
```
{: codeblock}
