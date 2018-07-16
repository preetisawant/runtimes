---

copyright:
  years: 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utiliser Dynatrace pour surveiller Node.js dans {{site.data.keyword.cloud_notm}}
{: #using_dynatrace}

Dynatrace est un service tiers qui offre une fonction de surveillance pour votre appli. Vous pouvez intégrer Dynatrace à votre application Node.js, mais IBM ne fournit pas de prise en charge pour les services tiers. Voir [Services tiers](../common/buildpackSupport.html#third-party) pour plus d'informations.

Pour des informations concernant Dynatrace et ses octrois de licence, voir [Dynatrace Application Monitoring ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.dynatrace.com/en/products/application-monitoring.html).

Lorsque votre application Node.js est configurée pour utiliser Dynatrace, le contexte d'exécution Node.js acquiert un script d'installation de plateforme Dynatrace sous forme de services (PaaS) depuis le site de Dynatrace et exécute cet agent Dynatrace avec votre application. Pour intégrer Dynatrace à votre application, vous devez créer un service fourni par l'utilisateur puis lier ce service à votre application.

## Intégration de Dynatrace à votre application

1. Connectez-vous à votre compte Dynatrace et générez un jeton PaaS. Pour plus de détails, voir la section [Generate PaaS token ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.dynatrace.com/support/help/cloud-platforms/cloud-foundry/how-do-i-monitor-cloud-foundry-applications/) de la documentation de surveillance d'application Cloud Foundry Dynatrace.

  Prenez soin de noter vos ID environnement et jeton.
1. Créez un service fourni par l'utilisateur qui pointe sur vos données d'identification Dynatrace en exécutant la commande suivante. Le nom du service doit comporter la chaîne `dynatrace`, par exemple `dynatrace-service`.

    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken"
    ```
    {: codeblock}
    
    **Remarque :** Ne remplacez pas `environmentid` ou `apitoken` par vos données d'identification. Une fois la commande lancée, vous serez invité à indiquer ces valeurs.

    Si vous utilisez Dynatrace Managed, ajoutez également la zone `apiurl`, qui spécifie le point de terminaison d'API de votre serveur géré.
    
    ```
    ibmcloud cf cups dynatrace-service -p "environmentid, apitoken, apiurl"
    ```
    {: codeblock}
    
    Lorsque vous êtes invité à exécuter la commande, définissez `apiurl` sur `https://<YourManagedServerURL>/e/<environmentID>/api`.
    
1. Après avoir envoyé votre application par commande push vers {{site.data.keyword.Bluemix_notm}}, associez-lui le service fourni par l'utilisateur que vous avez créé. Par exemple :
    ```
    ibmcloud cf bs myApp dynatrace-service
    ```
    {: codeblock}

    **Remarque** : Vous devez reconstituer votre application après avoir associé le service.

   Ou bien, vous pouvez lier le service à votre application en ajoutant le nom de votre service fourni par l'utilisateur à la section `service` du fichier `manifest.yml` de votre application.
   ```yaml
   ---
    applications:
    - path: .
      memory: 256M
      instances: 1
      name: myApp
      host: myApp
      disk_quota: 1024M
    services:
      - dynatrace-service
   ```
   {: codeblock}
