---

copyright:
  years: 2017
lastupdated: "2017-10-26"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utiliser votre propre JRE
{: #using_own_jre}

Vous pouvez exécuter votre application Liberty sur {{site.data.keyword.Bluemix}} avec votre propre JRE. Pour mettre votre
JRE à la disposition de votre application, vous devez effectuer les tâches suivantes.
* Héberger le JRE à un endroit d'où il pourra être téléchargé par le pack de construction.
* Héberger un fichier `index.yml` fournissant l'emplacement du JRE.
* Configurer votre application pour qu'elle utilise votre JRE.

## Héberger le JRE et le fichier `index.yml`
{: #hosting_jre}

Le fichier du JRE doit être hébergé sur un serveur web auprès duquel le pack de construction Liberty pourra le récupérer. Vous pouvez
l'héberger directement sur {{site.data.keyword.Bluemix_notm}} avec les fonctions disponibles sur le serveur, ou vous pouvez l'héberger dans un endroit disponible publiquement. Le serveur doit être configuré avec un fichier `index.yml` qui spécifie les détails relatifs au fichier du JRE.

Effectuez les étapes suivantes pour héberger le JRE et le fichier `index.yml` :
  1. Procurez-vous le JRE, qui doit être de la version à utiliser sur un système d'exploitation UNIX 64 bits et fourni dans un fichier `tar.gz`.
  2. Hébergez le fichier du JRE à un endroit d'où le pack de construction Liberty pourra le récupérer.
  3. Fournissez un fichier `index.yml` à l'emplacement d'hébergement. Le fichier `index.yml` doit
contenir une entrée composée de l'ID de version du JRE suivi d'un signe deux-points et de l'URL complète de l'endroit où se trouve le fichier du JRE.
    * Définissez la version du JRE dans le fichier `index.yml`.

    ```
    ---
   jre_version: https://hostingLocation/jreName.tar.gz
    ```
    {: codeblock}

    * Incluez l'ID de version du JRE et l'emplacement complet du fichier du JRE.  Par exemple :

    ```
    ---
       1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```
    {: codeblock}

## Configuration de l'application
{: #configure_app}

Pour configurer le pack de construction afin qu'il utilise un JRE alternatif, vous devez définir deux variables d'environnement
sur l'application Liberty. La variable **JBP_CONFIG_OPENJDK** doit identifier
l'emplacement du fichier `index.yml`. La variable **JVM**
doit avoir la valeur *openjdk*. Pour plus d'informations sur le format des chaînes
de version (valeur-version), consultez la documentation de Cloud Foundry sur [Version Syntax and Ordering and Wildcards ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/util-repositories.md){: new_window}.

La valeur de la variable
**JBP_CONFIG_OPENJDK** est l'emplacement du fichier `index.yml` et la version de JRE à choisir dans le
fichier index.yml.

```
'{repository_root: "https://locationToIndexYml", version: version-value}'
```
{: codeblock}

Emettez la commande `cf se myAPP` pour fixer la valeur de la variable **JBP_CONFIG_OPENJDK**. Par exemple :
```
$ cf se myApp JBP_CONFIG_OPENJDK '{repository_root: "https://myHostingApp.ng.bluemix.net", version: 1.8.+}'
```
{: codeblock}

L'URL qui suit *repository_root* n'inclut pas le nom de fichier `index.yml`. **Elle pointe seulement sur le répertoire qui contient le fichier `index.yml` et non sur ce dernier.

Pour définir la variable d'environnement JVM, émettez la commande suivante :
```
$ cf se myApp JVM 'openjdk'
```
{: codeblock}

**Remarque** : Après avoir défini les variables d'environnement, pour qu'elles soient prises en compte, reconstituez votre application.

## Vérifier
{: #confirmation}

Pour vérifier que Liberty utilise bien le JRE attendu, consultez le fichier journal de préproduction (staging). Recherchez-y un message indiquant que le serveur a téléchargé le pack de construction à partir de l'emplacement désigné dans le fichier `index.yml`. Voici un exemple de sortie possible lorsque Liberty utilise bien le JRE prévu.
```
 -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}
