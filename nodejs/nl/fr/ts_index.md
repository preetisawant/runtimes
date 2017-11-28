---

copyright:
  years: 2017
lastupdated: "2017-09-18"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Traitement des incidents liés à SDK for Node.js
{: #ts}


Voici les réponses aux questions fréquemment posées concernant le traitement des incidents liés à l'utilisation de SDK for Node.js sur {{site.data.keyword.Bluemix}}.
{:shortdesc}

## L'application ne démarre pas et l'erreur “No space left on device” (plus d'espace sur l'appareil) est retournée
{: #no_space_left_on_device}


Une application Node.js ne parvient pas démarrer avec l'erreur "No space left on device" (plus d'espace sur l'appareil). Par exemple, l'erreur figurant dans les journaux est similaire à l'erreur suivante :
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

Des applications Node.js utilisant une version de NPM antérieure à la version 3 consomment plus d'espace en téléchargeant leurs dépendances.
{: tsCauses}

Modifiez le fichier package.json de votre application afin d'utiliser NPM version 3 ou version ultérieure.
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

## Redémarrage de l'application en raison de contraintes de mémoire
{: #oom}

Node.js ne connaît pas la quantité de mémoire disponible pour l'application, donc le récupérateur de place risque de ne pas s'exécuter avant l'épuisement de la mémoire.

```
2017-09-01T11:00:42.19-0400 [APP/PROC/WEB/0]OUT Exit status 137
2017-09-01T11:00:42.23-0400 [CELL/0]     OUT Exit status 0
2017-09-01T11:00:42.27-0400 [CELL/0]     OUT Destroying container
2017-09-01T11:00:42.34-0400 [API/0]      OUT Process has crashed with type: "web"
2017-09-01T11:00:42.36-0400 [API/0]      OUT App instance exited with guid eecfba3b-430c-4a6b-b71f-ac72816fe152 payload: {"instance"=>"77dbb981-16d0-3a05-3235-9a4b", "index"=>0, "reason"=>"CRASHED", "exit_description"=>"2 error(s) occurred:\n\n* 2 error(s) occurred:\n\n* Exited with status 137 (out of memory)\n* cancelled\n* cancelled", "crash_count"=>1, "crash_timestamp"=>1504278042244633291, "version"=>"6497b5b5-67d4-4c5a-b1af-362e522a029d"}
2017-09-01T11:00:43.35-0400 [CELL/0]     OUT Successfully destroyed container
```
{: codeblock}

Une solution possible consiste à définir l'option `--max_old_space_size` dans la commande de démarrage de l'application dans le fichier package.json. Cette option représente une partie de l'encombrement mémoire de l'application et doit être définie avec une valeur inférieure à la mémoire totale disponible pour l'application. Lisez l'article [Large memory spikes and Heroku](https://github.com/nodejs/node/issues/3370) pour approfondir cette rubrique.
```
  "scripts": {
    "start": "node --max_old_space_size=800 server.js"
  }
```
{: codeblock}
