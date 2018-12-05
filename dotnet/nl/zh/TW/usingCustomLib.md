---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 使用自訂原生程式庫
{: #use_customlib}

某些程式庫可能需要使用 NuGet 套件及一些原生程式庫檔案（`.so` 檔案）。  

若要使用這些程式庫搭配建置套件，請將它們放在應用程式根資料夾內的 `ld_library_path` 資料夾。在編譯打包期間，此建置套件會將此路徑自動新增至 `LD_LIBRARY_PATH` 環境變數。  

或者，您也可以在應用程式的 `manifest.yml` 檔案中指定 `LD_LIBRARY_PATH` 環境變數，或是使用 `ibmcloud cf set-env` 指令，以使用與 `ld_library_path` 不同的資料夾名稱。在此情況下，建置套件會將此自訂路徑附加至建置套件所產生的 `LD_LIBRARY_PATH`。
