---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-14"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Fonctions Liberty prises en charge dans {{site.data.keyword.cloud_notm}}
{: #liberty_features}

L'environnement d'exécution instantané Liberty for Java inclut un sous-ensemble des
fonctions de Liberty. Certaines fonctions fournies par Liberty ne sont pas disponibles dans Liberty for Java, car elles ne s'appliquent pas à l'environnement cloud.

Les fonctions incluses suivantes sont spécifiques à {{site.data.keyword.Bluemix_notm}} :
* appstate-2.0
* cloudAutowiring-1.0
* logAnalysis-1.0

Un sous-ensemble des fonctions disponibles sont activées par défaut lors du déploiement des fichiers WAR ou EAR.  Voir [Applications autonomes](optionsForPushing.html#stand_alone_apps) pour plus de détails.

L'exécution Liberty for Java met également à disposition quelques fonctions bêta Liberty, qui ne sont pas listées mais figurant dans [Utilisation des fonctions bêta](/docs/runtimes/liberty/usingBetaFeatures.html).

Gardez à l'esprit qu'un serveur ne peut pas charger de fonctions incompatibles, assurez-vous donc qu'il est configuré pour n'activer que des fonctions qui sont compatibles. Voir
    <a href="https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html">Combinaisons de fonctions Java EE 6 et 7 prises en charge</a>.

Pour afficher une liste complète des fonctions disponibles dans Liberty accompagnée d'informations relatives aux versions Java EE versions et d'autres détails, voir [Fonctions Liberty](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)
dans IBM Knowledge Center.

Les applications qui utilisent des EJB distants peuvent être déployées dans {{site.data.keyword.Bluemix_notm}}. Toutefois, les EJB distants ne sont pas accessibles à distance avec le
protocole CORBA/IIOP en raison de restrictions de port dans l'environnement {{site.data.keyword.Bluemix_notm}}.

## Index des fonctionnalités Liberty
{: #libertyfeat_index}
Passez à la section appropriée de la liste des fonctionnalités en utilisant l'index suivant. Vous pouvez sinon parcourir la [Liste des fonctionnalités Liberty](#libertyfeat_list).

### A à E
* [A](#libertyfeat_A)
* [B](#libertyfeat_B)
* [C](#libertyfeat_C)
* [E](#libertyfeat_E)

### F à J
* [F](#libertyfeat_F)
* [J](#libertyfeat_J)

### K à O
* [L](#libertyfeat_L)
* [M](#libertyfeat_M)
* [O](#libertyfeat_O)

### P à T
* [P](#libertyfeat_P)
* [R](#libertyfeat_R)
* [S](#libertyfeat_S)
* [T](#libertyfeat_T)

### U à Z
* [W](#libertyfeat_W)


## Liste des fonctionnalités Liberty
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
* jms-1.1
* jms-2.0
* jmsMdb-3.1
* jmsMdb-3.2
* jndi-1.0
* jpa-2.0
* jpa-2.1
* jsf-2.0
* jsf-2.2
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
* managedBeans-1.0
* mdb-3.1
* mdb-3.2
* mediaServerControl-1.0     
* microprofile-1.0
* microprofile-1.2
* mongodb-2.0
* monitor-1.0

### O
{: #libertyfeat_O}
* oauth-2.0
* openapi-3.0
* openid-2.0
* openidConnectClient-1.0
* openidConnectServer-1.0
* osgi.jpa-1.0
* osgiAppIntegration-1.0
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

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/cwlp_about.html)
