---

copyright:
  years: 2015, 2018
lastupdated: "2018-03-16"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# {{site.data.keyword.cloud_notm}}에서 지원되는 Liberty 기능
{: #liberty_features}

Liberty for Java 인스턴트 런타임에는 Liberty 기능의 서브세트가 포함됩니다.  Liberty에서 제공하는 일부 기능은 클라우드 환경에서 적용할 수 없기 때문에 Liberty for Java 인스턴트 런타임에서 사용할 수 없습니다.

{{site.data.keyword.Bluemix_notm}}에 특정한 다음 기능이 포함됩니다.
* appstate-2.0
* cloudAutowiring-1.0
* logAnalysis-1.0

WAR 또는 EAR 파일을 배치하면 사용 가능한 기능 서브세트가 기본적으로 사용됩니다.  세부사항은 [독립형 앱](optionsForPushing.html#stand_alone_apps)을 참조하십시오.

Liberty for Java 런타임에서는 일부 Liberty 베타 기능도 사용 가능합니다. 해당 기능은 나열되어 있지 않지만 [베타 기능 사용](/docs/runtimes/liberty/usingBetaFeatures.html)에서 이를 찾을 수 있습니다.

서버는 호환 불가능한 기능은 로드할 수 없으므로 호환 가능한 기능만 사용하도록 구성해야 합니다. 
    <a href="https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html">지원되는 Java EE 6 및 7 기능 조합</a>을 참조하십시오.

Java EE 버전 및 기타 정보와 함께 Liberty에서 사용 가능한 전체 기능 목록을 보려면 IBM Knowledge Center에서
[Liberty 기능](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)을
참조하십시오.

원격 EJB를 사용하는 애플리케이션은 {{site.data.keyword.Bluemix_notm}}에 배치될 수 있습니다.
그러나 원격 EJB는 {{site.data.keyword.Bluemix_notm}} 환경의 포트 제한사항 때문에
CORBA/IIOP 프로토콜로 원격 액세스가 가능하지 않습니다.

## Liberty 기능 색인
{: #libertyfeat_index}
다음 색인을 사용하여 기능 목록의 섹션으로 건너뛰거나 [Liberty for Java 기능 목록](#libertyfeat_list)을 검토할 수 있습니다. 

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


## Liberty 기능 목록
{: #libertyfeat_list}

### A
{: #libertyfeat_A}

* apiDiscovery-1.0
* appSecurity-1.0
* appSecurity-2.0
* appstate-1.0
* appstate-2.0

### B
{: #libertyfeat_B}

* batch-1.0
* batchManagement-1.0
* beanValidation-1.1
* bells-1.0
* blueprint-1.0

### C
{: #libertyfeat_C}

* cdi-1.0
* cdi-1.2
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
* javaMail-1.5
* jaxb-2.2
* jaxrs-1.1
* jaxrs-2.0
* jaxrsClient-2.0
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
* jsf-2.0
* jsf-2.2
* jsfContainer-2.2
* json-1.0
* jsonp-1.0
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
* mongodb-2.0
* monitor-1.0
* mpConfig-1.1
* mpFaultTolerance-1.0
* mpHealth-1.0
* mpJwt-1.0
* mpMetrics-1.0

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
* websocket-1.0
* websocket-1.1
* wmqJmsClient-1.1
* wmqJmsClient-2.0
* wsAtomicTransaction-1.2
* wsSecurity-1.1
* wsSecuritySaml-1.1

# 관련 링크
{: #rellinks notoc}
## 일반
{: #general notoc}
* [Liberty 런타임](index.html)
* [Liberty 개요](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
