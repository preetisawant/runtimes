---

copyright:
  years: 2015, 2019
lastupdated: "2019-02-01"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# {{site.data.keyword.cloud_notm}} 中支援的 Liberty 特性
{: #liberty_features}

Liberty for Java 運行環境包括 Liberty 特性的子集。若要使用運行環境中未包含的特性，請參閱[安裝 Liberty 特性](/docs/runtimes/liberty/installFeatures.html)。如需 Liberty 中可用特性的完整清單，以及 Java EE 版本及其他資訊，請參閱
[Liberty features ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)。

## 雲端特定的特性
{:#cloud-features}

下列是已包含且 {{site.data.keyword.Bluemix_notm}} 特有的特性：
* appstate-1.0
* appstate-2.0
* cloudAutowiring-1.0 
* logAnalysis-1.0

當部署 WAR 或 EAR 檔案時，依預設會啟用可用特性的子集。如需詳細資料，請參閱[獨立式應用程式](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)。

Liberty for Java 運行環境也會讓部分 Liberty 測試版特性可供使用。這些特性列在[使用測試版特性](/docs/runtimes/liberty/usingBetaFeatures.html)。

## 特性相容性
{:#feature-compatibility}

Liberty 提供的部分特性無法在 Liberty for Java 運行環境中使用，因為它們不適用於雲端環境。

請記住，伺服器無法載入不相容的特性，因此務必將它配置為僅啟用相容的特性。請參閱[支援的 Java EE 6 及 7 特性組合](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html)以及[支援的 Java EE 7 及 8 特性組合](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos_7_8.html)。

使用遠端 EJB 的應用程式可以部署至 {{site.data.keyword.Bluemix_notm}}，不過，由於 {{site.data.keyword.Bluemix_notm}} 環境中的埠限制，無法使用 CORBA/IIOP 通訊協定來遠端存取這些遠端 EJB。

## Liberty 特性索引
{: #libertyfeat_index}

您可以使用下列索引以跳過特性清單一節，也可以瀏覽 [Liberty for Java 特性清單](#libertyfeat_list)。

### A-E
* [A](#libertyfeat_A)
* [B](#libertyfeat_B)
* [C](#libertyfeat_C)
* [E](#libertyfeat_E)

### F-J
* [F](#libertyfeat_F)
* [H](#libertyfeat_H)
* [J](#libertyfeat_J)

### K-O
* [L](#libertyfeat_L)
* [M](#libertyfeat_M)
* [O](#libertyfeat_O)

### P-T
* [P](#libertyfeat_P)
* [R](#libertyfeat_R)
* [S](#libertyfeat_S)
* [T](#libertyfeat_T)

### U - Z
* [W](#libertyfeat_W)


## Liberty 特性清單
{: #libertyfeat_list}

### A
{: #libertyfeat_A}

* apiDiscovery-1.0
* appSecurity-1.0
* appSecurity-2.0
* appSecurity-3.0
* appstate-1.0
* appstate-2.0

### B
{: #libertyfeat_B}

* batch-1.0
* batchManagement-1.0
* beanValidation-1.1
* beanValidation-2.0
* bells-1.0
* blueprint-1.0

### C
{: #libertyfeat_C}

* cdi-1.0
* cdi-1.2
* cdi-2.0
* cloudant-1.0
* cloudAutowiring-1.0 
* concurrent-1.0
* constrainedDelegation-1.0
* couchdb-1.0

### E
{: #libertyfeat_E}

* ejb-3.2
* ejbLite-3.1
* ejbLite-3.2
* el-3.0
* eventLogging-1.0

### F
{: #libertyfeat_f}

* federatedRegistry-1.0

### H
{: #libertyfeat_h}

* httpWhiteboard-1.0

### J
{: #libertyfeat_J}
* jacc-1.5
* jaspic-1.1
* javaee-7.0
* javaee-8.0
* javaMail-1.5
* javaMail-1.6
* jaxb-2.2
* jaxrs-1.1
* jaxrs-2.0
* jaxrs-2.1
* jaxws-2.2 
* jca-1.6 
* jca-1.7
* jcaInboundSecurity-1.0
* jdbc-4.0
* jdbc-4.1
* jdbc-4.2
* jms-1.1
* jms-2.0
* jmsMdb-3.1 
* jmsMdb-3.2
* jndi-1.0
* jpa-2.0
* jpa-2.1
* jpa-2.2
* jsf-2.0
* jsf-2.2
* jsf-2.3
* jsfContainer-2.2
* json-1.0 
* jsonb-1.0
* jsonp-1.0
* jsonp-1.1
* jsp-2.2
* jsp-2.3
* jwt-1.0

### L
{: #libertyfeat_L}
* ldapRegistry-3.0 
* localConnector-1.0 
* logAnalysis-1.0
* logstashCollector-1.0

### M
{: #libertyfeat_M}
* managedBeans-1.0
* mdb-3.1
* mdb-3.2 
* mediaServerControl-1.0     
* microProfile-1.0
* microProfile-1.2
* microProfile-1.3
* microProfile-1.4
* microProfile-2.0
* microProfile-2.1
* mongodb-2.0 
* monitor-1.0 

### O
{: #libertyfeat_O}
* oauth-2.0 
* openapi-3.0
* openapi-3.1
* openid-2.0 
* openidConnectClient-1.0 
* openidConnectServer-1.0 
* opentracing-1.0
* osgi.jpa-1.0 
* osgiAppIntegration-1.0
* osgiBundle-1.0
* osgiConsole-1.0 

### P
{: #libertyfeat_P}
* passwordUtilities-1.0

### R
{: #libertyfeat_R}
* requestTiming-1.0
* restConnector-1.0 
* restConnector-2.0
* rtcomm-1.0
* rtcommGateway-1.0

### S
{: #libertyfeat_S}
* samlWeb-2.0
* scim-1.0
* servlet-3.0
* servlet-3.1
* servlet-4.0
* sessionDatabase-1.0 
* sipServlet-1.1
* socialLogin-1.0
* spnego-1.0
* ssl-1.0 

### T
{: #libertyfeat_T}
* timedOperations-1.0 
* transportSecurity-1.0

### W
{: #libertyfeat_W}
* wab-1.0 
* wasJmsClient-1.1 
* wasJmsClient-2.0
* wasJmsSecurity-1.0 
* wasJmsServer-1.0 
* webCache-1.0 
* webProfile-6.0 
* webProfile-7.0
* webProfile-8.0
* websocket-1.0
* websocket-1.1
* wmqJmsClient-1.1 
* wmqJmsClient-2.0
* wsAtomicTransaction-1.2
* wsSecurity-1.1
* wsSecuritySaml-1.1
