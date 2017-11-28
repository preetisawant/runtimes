---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Startbefehl verwenden
{: #startup_commmand}

Für die Angabe eines Startbefehls für Ihre {{site.data.keyword.Bluemix}}-Node.js-Anwendung empfiehlt sich die Verwendung einer **Procfile**- oder einer **package.json**-Datei.
{: shortdesc}

1. Geben Sie in Ihrer **Procfile** einen Startbefehl im nachfolgenden Format an. Dabei ist _app.js_ das js-Startscript für Ihre Anwendung.
```
web: node app.js
```
{: codeblock}

1. Speichern Sie die **Procfile** im Stammverzeichnis Ihrer Anwendung.

Wenn keine **Procfile**-Datei vorhanden ist, prüft das IBM Bluemix-Node.js-Buildpack, ob der Eintrag 'scripts.start' in der Datei **package.json** vorhanden ist. Im unten stehenden Beispiel ist 'app.js' wieder das js-Startscript für Ihre Anwendung.
```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

Wenn ein Eintrag für ein Startscript in der Datei **package.json** vorhanden ist, wird automatisch eine **Procfile** erstellt. Der Inhalt der automatisch generierten **Procfile** ist wie folgt:
```
    web: npm start
```
{: codeblock}

Weitere Informationen zur **Procfile**-Datei und zur **package.json**-Datei finden Sie in [Tips for Node.js Applications ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).
