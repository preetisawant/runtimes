---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}

{{site.data.keyword.Bluemix}} 上的 PHP 運行環境是採用 php_buildpack 技術。
php_buildpack 為 PHP 應用程式提供完整的運行環境。
{: shortdesc}

在下列狀況下將使用 php_buildpack：
* 應用程式包含 composer.json 檔案，或是
* 應用程式包含 *.php 檔案，或是
* 應用程式在其 [options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html) 檔案中定義了 ${WEBDIR} 變數，且該變數是設為應用程式內的現有目錄。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 PHP 入門範本應用程式。PHP 入門範本應用程式是簡單的 PHP 應用程式，提供可以讓您用於應用程式的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 {{site.data.keyword.Bluemix}} 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](../common/starter_app_usage.html)。

## 在應用程式的所有頁面上施行 HTTPS
{: #enforce_https}

使用 Apache 在 {{site.data.keyword.Bluemix_notm}} 中執行時，若要在應用程式的所有頁面上施行 HTTPS 而非 HTTP，需要對您的 ".htaccess" 檔案進行下列變更。此規則只有在 {{site.data.keyword.Bluemix_notm}} 中執行時，才適用於未使用 HTTPS 提出的任何要求。

```
RewriteCond %{HTTP:X-Forwarded-Proto} !=https [NC]
RewriteCond %{ENV:BLUEMIX_REGION} !^$
RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

## 運行環境版本
{: #runtime_versions}

您可以在 composer.json 檔案中指定應用程式要使用的 PHP 版本。例如：

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
如需相關資訊，請參閱 [Composer 套件鏈結 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://getcomposer.org/doc/04-schema.md#package-links)。



如果未指定版本，依預設會選擇 5.6.34 版。

### 可用的版本：
{: #available_versions}

目前安裝在 {{site.data.keyword.Bluemix}} 中的 [PHP 建置套件](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.51)提供下列 PHP 版本：

* 5.6.33
* 5.6.34
* 7.0.27
* 7.0.28
* 7.1.14
* 7.1.15
* 7.2.2
* 7.2.3

如果您的應用程式需要未列出的 PHP 版本，可以使用外部 [PHP 建置套件](https://github.com/cloudfoundry/php-buildpack.git)來部署該應用程式。
