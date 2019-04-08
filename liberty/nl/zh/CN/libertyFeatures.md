---

copyright:
  years: 2015, 2019
lastupdated: "2019-02-01"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# {{site.data.keyword.cloud_notm}} 中支持的 Liberty 功能
{: #liberty_features}

Liberty for Java 运行时包含 Liberty 功能的子集。要使用运行时中不包含的功能，请参阅[安装 Liberty 功能](/docs/runtimes/liberty/installFeatures.html)。有关 Liberty 中可用功能的完整列表，以及 Java EE 版本和其他信息，请参阅
[Liberty 功能部件 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)。

## 云特定的功能
{:#cloud-features}

其中包含以下功能，这些功能特定于 {{site.data.keyword.Bluemix_notm}}：
* appstate-1.0
* appstate-2.0
* cloudAutowiring-1.0 
* logAnalysis-1.0

缺省情况下，部署 WAR 或 EAR 文件时，将启用可用的功能子集。请参阅[独立应用程序](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps)，以获取详细信息。

Liberty for Java 运行时还提供了某些 Liberty Beta 功能。[使用 Beta 功能](/docs/runtimes/liberty/usingBetaFeatures.html)中列出了这些功能。

## 功能兼容性
{:#feature-compatibility}

Liberty 提供的某些功能在 Liberty for Java 运行时中不可用，因为这些功能在云环境中不适用。

请记住，服务器无法装入不兼容的功能，因此请确保将其配置为仅启用兼容的功能。请参阅[受支持的 Java EE 6 与 Java EE 7 功能部件组合](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html)和[支持的 Java EE 7 和 8 功能部件组合](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos_7_8.html)。

使用远程 EJB 的应用程序可以部署到 {{site.data.keyword.Bluemix_notm}}，但是，由于 {{site.data.keyword.Bluemix_notm}} 环境中的端口限制，不可通过 CORBA/IIOP 协议来远程访问远程 EJB。

## Liberty 功能索引
{: #libertyfeat_index}

可以使用以下索引跳至功能列表的相应部分，也可以浏览整个 [Liberty for Java 功能列表](#libertyfeat_list)。

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


## Liberty 功能列表
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
