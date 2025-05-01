---

copyright:
  years:  2021, 2025
lastupdated: "2025-05-01"

keywords:

subcollection: atracker


---

{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.cloud_notm}} services that generate events that are managed through {{site.data.keyword.atracker_short}}
{: #cloud_services_atracker}

List of {{site.data.keyword.cloud}} services that generate auditing events that you can manage through {{site.data.keyword.atracker_full_notm}}.
{: shortdesc}

{{site.data.keyword.atracker_short}} routes events based on the location that is specified in the `logSourceCRN` field included in the event. You can define a target, the resource where events are routed to, in any {{site.data.keyword.atracker_short}} supported region. However, the target resource can be located in any region where that type of target is supported, in the same account or in a different account. You can define rules to determine where auditing events are to be routed by configuring 1 or more routes in the account. You can define rules for managing global events and location-based events that are generated in regions where {{site.data.keyword.atracker_short}} is supported.
{: important}

## Analytics services
{: #cloud_services_analytics}

The following table lists analytics services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.iae_full}}](/docs/AnalyticsEngine?topic=AnalyticsEngine-getting-started) | `ibmanalyticsengine` | [Location-based events](/docs/AnalyticsEngine?topic=AnalyticsEngine-at_events-serverless) |
{: caption="List of analytics services" caption-side="top"}

## Classic services
{: #classic}

The following table lists services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.baremetal_long}} (Classic)](/docs/bare-metal?topic=bare-metal-about-bm#about-bm) | `audit-log` | [Location-based events](/docs/bare-metal?topic=bare-metal-bm-at-events) |
{: caption="List of classic services" caption-side="top"}


## Compute serverless services
{: #serverless}

The following table lists serverless compute services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.codeenginefull}}](/docs/codeengine?topic=codeengine-getting-started)| `codeengine`  | [Location-based events](/docs/codeengine?topic=codeengine-at_events) |
| [{{site.data.keyword.satellitelong}}](/docs/satellite?topic=satellite-getting-started) | `satellite` | [Location-based events](/docs/satellite?topic=satellite-at_events) |
{: caption="List of serverless compute services" caption-side="top"}



## Container services
{: #container}

The following table lists container platform services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.registrylong}}](/docs/Registry?topic=Registry-getting-started) | `container-registry` | [Location-based events](/docs/Registry?topic=Registry-at_events) |
| [{{site.data.keyword.containerlong}}](/docs/containers?topic=containers-getting-started) | `containers-kubernetes` | [Location-based events](/docs/containers?topic=containers-at_events_ref) |
| [{{site.data.keyword.openshiftlong}}](/docs/openshift?topic=openshift-getting-started) | `openshift` | [Location-based events](/docs/openshift?topic=openshift-at_events) |
{: caption="Container events" caption-side="top"}


## Database services
{: #database}

The following table lists database services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.cloudantfull}}](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant) | `cloudantnosqldb`  | [Location-based events](/docs/Cloudant?topic=Cloudant-at_events) |
| [{{site.data.keyword.dashdblong_notm}}](/docs/Db2whc?topic=Db2whc-getting-started) | `dashdb` | [Global events](/docs/atracker?topic=atracker-at_events_dashdb) |
| [{{site.data.keyword.databases-for-postgresql_full}}](/docs/databases-for-postgresql?topic=databases-for-postgresql-getting-started) | `databases-for-postgresql` | [Location-based events](/docs/databases-for-postgresql?topic=databases-for-postgresql-at_events) |
| [{{site.data.keyword.databases-for-redis_full_notm}}](/docs/databases-for-redis?topic=databases-for-redis-getting-started) | `databases-for-redis` | [Location-based events](/docs/databases-for-redis?topic=databases-for-redis-at_events) |
| [{{site.data.keyword.databases-for-etcd_full_notm}}](/docs/databases-for-etcd?topic=databases-for-etcd-getting-started) | `databases-for-etcd` | [Location-based events](/docs/databases-for-etcd?topic=databases-for-etcd-at_events) |
| [{{site.data.keyword.databases-for-elasticsearch_full_notm}}](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-getting-started) | `databases-for-elasticsearch` | [Location-based events](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-at_events) |
| [{{site.data.keyword.messages-for-rabbitmq_full}}](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-getting-started)  | `messages-for-rabbitmq` | [Location-based events](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-at_events) |
| [{{site.data.keyword.databases-for-mongodb_full_notm}}](/docs/databases-for-mongodb) | `databases-for-mongodb` | [Location-based events](/docs/databases-for-mongodb?topic=databases-for-mongodb-at_events) |
| [{{site.data.keyword.databases-for-mysql_full}}](/docs/databases-for-mysql) | `databases-for-mysql` | [Location-based events](/docs/databases-for-mysql?topic=databases-for-mysql-at_events) |
| [{{site.data.keyword.databases-for-enterprisedb_full}}](/docs/databases-for-enterprisedb?topic=databases-for-enterprisedb-getting-started) | `databases-for-enterprisedb-group` | [Location-based events](/docs/databases-for-enterprisedb?topic=databases-for-enterprisedb-at_events) |
{: caption="List of database services" caption-side="top"}


## Developer tools
{: #devops}

The following table lists developer tools and DevOps services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started)  | `schematics` | [Location-based events](/docs/schematics?topic=schematics-at_events) |
| [{{site.data.keyword.en_full}}](/docs/event-notifications?topic=event-notifications-getting-started) | `event-notifications`| Location-based events |
| [{{site.data.keyword.appconfig_full}}](/docs/app-configuration?topic=app-configuration-getting-started) | `apprapp`| [Location-based events](/docs/app-configuration?topic=app-configuration-at_events)|
| [{{site.data.keyword.cloud-shell_full}}](/docs/cloud-shell?topic=cloud-shell-getting-started) | `cloudshell` | [Location-based events](/docs/cloud-shell?topic=cloud-shell-at_events) |
{: caption="List of developer tools services" caption-side="top"}


The following table lists {{site.data.keyword.contdelivery_full}} services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.contdelivery_full}}](/docs/ContinuousDelivery?topic=ContinuousDelivery-getting-started) | `continuous-delivery` | [Location-based events](/docs/ContinuousDelivery?topic=ContinuousDelivery-at_events) |
| [Toolchain](/docs/ContinuousDelivery?topic=ContinuousDelivery-cd_about) | `toolchain` | [Location-based events](/docs/ContinuousDelivery?topic=ContinuousDelivery-at_events#at_actions_toolchain) |
{: caption="List of developer tools services" caption-side="top"}


## Integration services
{: #integration}

The following table lists integration services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.messagehub_full}}](/docs/EventStreams?topic=EventStreams-getting-started)| `messagehub` | [Location-based events](/docs/EventStreams?topic=EventStreams-at_events) |
| [MQ on IBM Cloud](/docs/mqcloud?topic=mqcloud-getting_started) |`mqcloud` | [Location-based events](/docs/mqcloud?topic=mqcloud-at_events) |
|[{{site.data.keyword.apiconnect_long}}](/docs/apiconnect?topic=apiconnect-getting-started)| `apiconnect` | [Location-based events](/docs/apiconnect?topic=apiconnect-at_events) |
{: caption="List of integration Cloud services" caption-side="top"}

## Network services
{: #network}

The following table lists network services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.BluDirectLink}} solution](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) | `directlink.dedicated` | [Global events](/docs/dl?topic=dl-at_events) |
| [{{site.data.keyword.tg_full}}](/docs/transit-gateway?topic=transit-gateway-getting-started) | `transit` | [Global events](/docs/transit-gateway?topic=transit-gateway-at_events) |
| [{{site.data.keyword.dns_full}}](/docs/dns-svcs?topic=dns-svcs-getting-started) | `dns-svcs` | [Global events](/docs/dns-svcs?topic=dns-svcs-at_events) |
| [{{site.data.keyword.cis_full}} (CIS)](/docs/cis?topic=cis-getting-started)| `internet-svcs` | [Global events](/docs/cis?topic=cis-at_events) |
{: caption="List of network services" caption-side="top"}


## Observability services
{: #observability}

The following table lists observability services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.atracker_full}}](/docs/atracker?topic=atracker-getting-started) | `atracker` | [Location-based events](/docs/atracker?topic=atracker-at_events). |
| [{{site.data.keyword.logs_routing_full}}](/docs/logs-router) | `log-router` | [Location-based events](/docs/logs-router?topic=logs-router-at_events). |
| [{{site.data.keyword.metrics_router_full}}](/docs/metrics-router?topic=metrics-router-getting-started) | `metrics-router` | [Location-based events](/docs/metrics-router?topic=metrics-router-at_events). |
| [{{site.data.keyword.mon_full}}](/docs/monitoring?topic=monitoring-getting-started) | `sysdig-monitor` | [Location-based events](/docs/monitoring?topic=monitoring-at_events) |
{: caption="List of observability services" caption-side="top"}


## Platform services
{: #platform_core_integrated}

The following table lists platform services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [Billing](/docs/account?topic=account-account-services&interface=ui#billing-acct-mgmt ) | `billing` | [Global events](/docs/atracker?topic=atracker-at_events_acc_mgt#at_events_acc_mgt_account) |
| [User management](/docs/account?topic=account-iamuserinv) | `user-management` | [Global events](/docs/atracker?topic=atracker-at_events_acc_mgt#at_events_acc_mgt_users) |
| [Provisioning](/docs/account?topic=account-manage_resource) | `provisioning` | [Global events](/docs/atracker?topic=atracker-at_events_rc#at_events_rc) |
| [Carbon Calculator](/docs/account?topic=account-what-is-cloud-calc) | `carbon-calculator` | [Global events](/docs/atracker?topic=atracker-at_events_acc_mgt#at_events_carbon_calculator) |
| [{{site.data.keyword.iamlong}}](/docs/account?topic=account-iamoverview)   | `iam-identity`   \n `iam-groups`   \n `iam-am` | [Global events](/docs/atracker?topic=atracker-at_events_iam) |
| [Global Search Service](/docs/account?topic=account-tag) | `global-search-tagging` | [Global events](/docs/atracker?topic=atracker-at_events_acc_mgt#at_events_acc_mgt_resources) |
| [Catalog Management](/docs/account?topic=account-filter-account)`[*]` | `globalcatalog-collection` | [Global events](/docs/atracker?topic=atracker-at_events_acc_mgt#at_events_catalog_management) |
| [Software instance](/docs/account?topic=account-sw-instance-details) `[*]` | `globalcatalog-instance` | [Global events](/docs/atracker?topic=atracker-at_events_acc_mgt#at_events_sw_instance) |
| [Context-based restrictions](/docs/account?topic=account-context-restrictions-whatis) | `context-based-restrictions` | [Global events](/docs/activity-tracker?topic=activity-tracker-events_context_based#restriction_rules_events) |
| [Projects](/docs/secure-enterprise?topic=secure-enterprise-understanding-projects) | `project` | [Global events](/docs/secure-enterprise?topic=secure-enterprise-at_events) |
{: caption="List of platform services" caption-side="top"}

`[*]` - Event routing available to {{site.data.keyword.at_full_notm}} only.
{: note}

## Security services
{: #security}

The following table lists security Cloud services that send auditing events:


| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.appid_full}}](/docs/appid?topic=appid-getting-started) | `appid` | [Location-based events](/docs/appid?topic=appid-at_events)   |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-get-started) | `hs-crypto` | [Location-based events](/docs/hs-crypto?topic=hs-crypto-at-events) |
| [{{site.data.keyword.secrets-manager_full}}](/docs/secrets-manager?topic=secrets-manager-getting-started) | `secrets-manager` |  [Location-based events](/docs/secrets-manager?topic=secrets-manager-at_events) |
| [{{site.data.keyword.keymanagementservicelong}}](/docs/key-protect?topic=key-protect-getting-started-tutorial#getting-started-tutorial) | `kms` | [Location-based events](/docs/key-protect?topic=key-protect-at-events) |
| [{{site.data.keyword.compliance_full}}](/docs/security-compliance?topic=security-compliance-getting-started) `[*]`| `compliance`  \n `security-advisor` | [Location-based events](/docs/security-compliance?topic=security-compliance-at_events) |
{: caption="List of security services" caption-side="top"}

`[*]` - Event routing available to {{site.data.keyword.at_full_notm}} only.
{: note}

## Storage services
{: #storage}


The following table lists storage services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.cos_full}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage)| `cloud-object-storage` | [Global and location-based events `[*]`](/docs/cloud-object-storage?topic=cloud-object-storage-at-events) |
| [{{site.data.keyword.cephaas_full}}](/docs/cephaas?topic=cephaas-getting-started)| `software-defined-storage` | [Global events](/docs/cephaas?topic=cephaas-at_events) |
{: caption="List of storage events" caption-side="top"}


`[*]` {{site.data.keyword.cos_full_notm}} (COS) generates global, and location-based events.
* By default, bucket management events such as the creation of a bucket are collected automatically.
* Collection of data events in your account is optional. You must configure each bucket to enable data events by selecting the option **Track data events**.


## VMware Solutions
{: #vmware_solutions}

With {{site.data.keyword.vmwaresolutions_full_notm}}, you can quickly and seamlessly integrate or migrate your on-premises VMware workloads to the {{site.data.keyword.cloud_notm}} by using the scalable, secure, and high-performance {{site.data.keyword.cloud_notm}} infrastructure and the industry-leading VMware hybrid virtualization technology. You can easily deploy your VMware virtual environments and manage the infrastructure resources on {{site.data.keyword.cloud_notm}}. At the same time, you can still use your familiar native VMware product console to manage the VMware workloads. [Learn more](https://www.ibm.com/products/vmware){: external}.

The following table lists VMware Solutions services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.vmwaresolutions_short}}](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview)   | `vmware-solutions` | [Global events](/docs/vmwaresolutions?topic=vmwaresolutions-at_events) |
| [{{site.data.keyword.cloud}} for VMware Shared](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview)      | `vmware-solutions` | [Location-based events](/docs/vmwaresolutions?topic=vmwaresolutions-at_events#at-events-vdc) |
| [KMIP for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_considerations) `[*]` | `vmware-solutions` | [Location-based events](/docs/vmwaresolutions?topic=vmwaresolutions-at_events#at-events-kmip) |
{: caption="List of VMware Solutions services" caption-side="top"}

`[*]` - Event routing available to {{site.data.keyword.at_full_notm}} only.
{: note}

## VMware Cloud Foundation as a Service 
{: #vmware_service}

{{site.data.keyword.vmware-service_notm}} provides the VMware Cloud Director™ platform as either a dedicated or shared managed service. IBM performs the configuration, hosting, operations, and lifecycle management of the VMware by Broadcom software so you can quickly deploy your VMware-based cloud computing environments. Compute resources are available as either dedicated or multitenant hosts that use {{site.data.keyword.cloud_notm}} bare metal servers.

The following table lists VMware Cloud Foundation (VCF) as a Service services that send auditing events:

| Service     | CRN service name | Events |
|-------------|--------------|--------|
| [VCF as a Service - Cloud Director sites](/docs/vmware-service?topic=vmware-service-tenant-ordering) | `vmware.directorsite` | ![Checkmark](/images/checkmark-icon.svg "Checkmark") | [Global events](/docs/vmware-service?topic=vmware-service-at_events#at-events-director-site) |
| [VCF as a Service - virtual data centers](/docs/vmware-service?topic=vmware-service-vdc-adding) | `vmware.vdc` | ![Checkmark](/images/checkmark-icon.svg "Checkmark") | [Global events](/docs/vmware-service?topic=vmware-service-at_events#at-events-vdc) |
{: caption="List of VCF as a Service services" caption-side="top"}

## VPC services
{: #vpc_services}

You can provision a Virtual Private Cloud (VPC) in the {{site.data.keyword.cloud_notm}} to run an isolated environment within the public cloud. VPC gives you the security of a private cloud, with the agility and ease of a public cloud. See [{{site.data.keyword.vpc_full}} Gen 2](/docs/vpc?topic=vpc-getting-started).


The following table lists VPC infrastructure services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [VPC](/docs/vpc?topic=vpc-getting-started) | `is` | [Location-based events](/docs/vpc?topic=vpc-at_events) |
| [Load Balancer](/docs/vpc?topic=vpc-load-balancers)| `is.load-balancer` | [Location-based events](/docs/vpc?topic=vpc-at_events#events-load-balancers) |
| [VPN](/docs/vpc?topic=vpc-using-vpn)| `is.vpn` | [Location-based events](/docs/vpc?topic=vpc-at_events) |
| [Client VPN](/docs/vpc?topic=vpc-vpn-client-to-site-overview)| `is.vpn-server` | [Location-based events](/docs/vpc?topic=vpc-at_events#events-vpn-server) |
{: caption="List of VPC infrastructure services (generation 2)" caption-side="top"}

## Watson AI
{: #watson_ai}

The following table lists Watson AI services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.dv_full_notm}}](/docs/data-virtualization?topic=data-virtualization-getting-started) | `data-virtualization` | [Location-based events](https://dataplatform.cloud.ibm.com/docs/content/wsj/admin/at-events.html?context=cpdaas&audience=wdp#dv){: external} |
| [{{site.data.keyword.DSX_short}}](https://dataplatform.cloud.ibm.com/docs/content/svc-welcome/wsl.html?context=wx){: external} | `data-science-experience` | [Location-based events](https://dataplatform.cloud.ibm.com/docs/content/wsj/admin/at-events.html?context=cpdaas&audience=wdp#shared){: external} |
| [{{site.data.keyword.knowledgestudiofull}}](/docs/watson-knowledge-studio) | `knowledge-studio` | [Location-based events](/docs/watson-knowledge-studio?topic=watson-knowledge-studio-activity-tracker-events) |
| [{{site.data.keyword.nlufull}}](/docs/natural-language-understanding) | `natural-language-understanding` | [Location-based events](/docs/natural-language-understanding?topic=natural-language-understanding-at_events) |
| [watsonx.governance ({{site.data.keyword.aios_full_notm}})](https://dataplatform.cloud.ibm.com/docs/content/svc-welcome/aiopenscale.html?context=wx&audience=wdp){: external} |
| [watsonx.orchestrate](https://www.ibm.com/docs/en/watsonx/watson-orchestrate/current?topic=getting-started-watsonx-orchestrate){: external} |  `watsonx-orchestrate` | [Location-based events](https://www.ibm.com/docs/en/SSAVQO/security/activity_tracker.html){: external} |
| [{{site.data.keyword.conversationfull}}](/docs/watson-assistant?topic=watson-assistant-getting-started) | `conversation`  | [Location-based events](/docs/watson-assistant?topic=watson-assistant-at-events) |
| [{{site.data.keyword.discoveryfull}}](/docs/discovery-data?topic=discovery-data-getting-started) | `discovery` | [Location-based events](/docs/discovery-data?topic=discovery-data-at_events)  |
| [{{site.data.keyword.speechtotextfull}}](/docs/speech-to-text?topic=speech-to-text-gettingStarted) | `speech-to-text` | [Location-based events](/docs/speech-to-text?topic=speech-to-text-at-events) |
| [{{site.data.keyword.texttospeechfull}}](/docs/text-to-speech?topic=text-to-speech-gettingStarted) | `text-to-speech` | [Location-based events](/docs/text-to-speech?topic=text-to-speech-at-events) |
{: caption="List of Watson AI services" caption-side="top"}


## Power IaaS services
{: #power_iaas_services}

Power Systems Virtual Server (PowerVS) projects deliver flexible compute capacity for Power Systems workloads. Integrated with the {{site.data.keyword.cloud_notm}} platform for on-demand provisioning, this offering provides a secure and scalable server virtualization environment that is built upon the advanced RAS features and leading performance of the Power Systems™ platform. See [{{site.data.keyword.powerSysFull}}](/docs/power-iaas?topic=power-iaas-getting-started).


The following table lists Power IaaS infrastructure services that send auditing events:

| Service     | CRN service name | Events |
|-------------|------------------|--------|
| [{{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-getting-started) | `power-iaas` | [Location-based events](/docs/power-iaas?topic=power-iaas-at-events) |
{: caption="List of Power Systems Virtual Server infrastructure services" caption-side="top"}
