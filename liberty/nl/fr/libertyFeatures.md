---

copyright:
  years: 2015, 2019
lastupdated: "2019-02-01"
subcollection: "liberty"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Fonctions Liberty prises en charge dans {{site.data.keyword.cloud_notm}}
{: #liberty_features}

L'environnement d'exécution Liberty for Java inclut un sous-ensemble des fonctions Liberty. Pour utiliser une fonction ne faisant pas partie de cet environnement, voir [Installation de fonctions Liberty](/docs/runtimes/liberty/installFeatures.html). Pour la liste complète des fonctions disponibles dans Liberty, ainsi que des versions de Java EE et d'autres informations, voir
[Fonctions Liberty ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html).

## Fonctions spécifiques au cloud
{:#cloud-features}

Les fonctions suivantes sont incluses et sont spécifiques à {{site.data.keyword.Bluemix_notm}} :
* appstate-1.0
* appstate-2.0
* cloudAutowiring-1.0
* logAnalysis-1.0

Un sous-ensemble des fonctions disponibles sont activées par défaut lors du déploiement des fichiers WAR ou EAR. Voir [Applications autonomes](/docs/runtimes/liberty/optionsForPushing.html#stand_alone_apps) pour plus de détails.

L'exécution Liberty for Java met également à disposition quelques fonctions bêta Liberty, Ces fonctions sont répertoriées dans [Utilisation des fonctions bêta](/docs/runtimes/liberty/usingBetaFeatures.html).

## Compatibilité des fonctions
{:#feature-compatibility}

Certaines fonctions fournies par Liberty ne sont pas disponibles dans Liberty for Java, car elles ne s'appliquent pas à l'environnement cloud.

Gardez à l'esprit qu'un serveur ne peut pas charger de fonctions incompatibles, assurez-vous donc qu'il est configuré pour n'activer que des fonctions qui sont compatibles. Voir [Combinaisons de fonctions Java EE 6 et 7 prises en charge](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html)
et [Combinaisons de fonctions Java EE 7 et 8 prises en charge](https://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos_7_8.html).

Les applications qui utilisent des EJB distants peuvent être déployées dans {{site.data.keyword.Bluemix_notm}}. Toutefois, les EJB distants ne sont pas accessibles à distance avec le protocole CORBA/IIOP
en raison de restrictions de port dans l'environnement {{site.data.keyword.Bluemix_notm}}.

## Index des fonctionnalités Liberty
{: #libertyfeat_index}

Passez à la section appropriée de la liste des fonctionnalités en utilisant l'index suivant. Vous pouvez sinon parcourir la [Liste des fonctionnalités Liberty for Java](#libertyfeat_list).

### A à E
* [A](#libertyfeat_A)
* [B](#libertyfeat_B)
* [C](#libertyfeat_C)
* [E](#libertyfeat_E)

### F à J
* [F](#libertyfeat_F)
* [H](#libertyfeat_H)
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
