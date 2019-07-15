---

copyright:
  years: 2017, 2018
lastupdated: "2018-07-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 撰寫安全的 Java Web 應用程式
{: #secure_java_web_app}

所有 Web 應用程式在設計及編碼時都必須注意安全，以避免引起嚴重安全漏洞。
{: shortdesc}

{{site.data.keyword.Bluemix}} 提供一種安全入門範本應用程式，可協助您撰寫更安全的 Liberty Java 程式碼，並避免大部分的「跨網站 Scripting (XSS)」問題。您可以下載此[安全入門範本應用程式](https://github.com/IBM-Cloud/java-secure-app)、進行建置，並在本端及 {{site.data.keyword.Bluemix_notm}} 上進行部署。

## 為何要撰寫安全 Web 應用程式
{: #why}

各種安全攻擊都會惡意探索安全漏洞。攻擊可能會竊取認證、導致資料及功能流失、中斷服務，以及損壞企業的信譽與營收。「跨網站 Scripting (XSS)」是在大部分 Web 應用程式中找到且必須避免的一種常見安全漏洞。

您可以使用此[安全入門範本應用程式](https://github.com/IBM-Cloud/java-secure-app)，而不必先學習 XSS 攻擊及改善技術的理論再開始 Web 應用程式開發。安全入門範本應用程式包括防止 XSS 之重要安全編碼作法的編碼範例，您可以在學習並套用 XSS 預防技術的同時就開始進行開發。

## 如何使用安全範例應用程式
{: #how}

您可以使用[安全入門範本應用程式](https://github.com/IBM-Cloud/java-secure-app)作為進行新 Liberty 應用程式開發的起點。請從學習應用程式中的 XSS 對策程式碼開始，然後將它套用至應用程式 API 的作業。安全入門範本應用程式中的對策可透過降低或防止 XSS 攻擊，來協助防止惡意使用者輸入損壞伺服器及瀏覽器上的應用程式。

首先，請下載此安全入門範本應用程式，然後透過處理 [getting-started-java](https://github.com/IBM-Cloud/get-started-java) 範例應用程式的相同方式，在 {{site.data.keyword.Bluemix_notm}} 或本端上進行建置並部署。移至[在 {{site.data.keyword.Bluemix_notm}} 上開始使用 Liberty](getting-started.html)，以進一步瞭解如何在 {{site.data.keyword.Bluemix_notm}} 上建置及部署應用程式。若要開始使用，您可以使用下列步驟來複製、建置及執行應用程式。

```
git clone https://github.com/IBM-Cloud/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
在下列網址檢視應用程式：http://localhost:9080/GetStartedSecureJava/



## 在應用程式的所有頁面上施行 HTTPS
{: #enforce_https}

若要在應用程式的所有頁面上施行 HTTPS 而非 HTTP，需要進行下列變更。

修改 server.xml，以啟用 `appSecurity-2.0` 特性：

```
  <featureManager>
    <feature>appSecurity-2.0</feature>
  </featureManager>
```

修改 web.xml 檔案，以包含下列安全限制：

```
  <security-constraint>
    <web-resource-collection>
      <web-resource-name>Entire Application</web-resource-name>
      <url-pattern>/*</url-pattern>
    </web-resource-collection>
    <user-data-constraint>
      <transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
  </security-constraint>
```

這可讓應用程式強制所有連線自動使用 HTTPS，且不容許任何 HTTP 連線。

## 進一步資訊
{: more}
安全入門範本應用程式包含 **BadServlet.java**。此應用程式顯示開發人員可能會不小心撰寫的不安全程式碼範例。

安全入門範本應用程式也會包含 **GoodServlet.java**，其中包括一些不錯的安全編碼作法（例如輸入驗證、輸出編碼、安全「HTTP 標頭」設定及「內容安全原則」）。這些作法是重要的 XSS 對策。套用它們，也可以緩和其他漏洞（例如，某種注入及目錄遍訪）。

請參閱 [XSS Prevention Cheat Sheet ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.owasp.org/index.php/XSS){: new_window}，以進一步瞭解 XSS 及其對策。
