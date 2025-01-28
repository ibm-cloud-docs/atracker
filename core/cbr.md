---

copyright:
  years:  2021, 2025
lastupdated: "2025-01-28"
keywords:

subcollection: atracker


---

{{site.data.keyword.attribute-definition-list}}


# Restricting access by context-based restrictions
{: #context-based-restrictions}

[Context-based restrictions (CBR)](/docs/account?topic=account-context-restrictions-whatis&interface=ui) provides a way for administrators to limit access to {{site.data.keyword.atracker_full}} destination resources or the {{site.data.keyword.atracker_full_notm}} public API. For general context-based restrictions instructions, see [Creating context-based restrictions](docs/account?topic=account-context-restrictions-create&interface=ui). 
{: shortdesc}

Any audit events generated come from the context-based restrictions service, and not {{site.data.keyword.atracker_full_notm}}. For more information, see [Monitoring context-based restrictions](/docs/account?topic=account-cbr-monitor).
{: note}

## Using context-based restrictions to protect destination resources
{: #cbr-config}

As an administrator, you can limit access to {{site.data.keyword.cos_full_notm}}, {{site.data.keyword.logs_full_notm}}, and {{site.data.keyword.messagehub_full}} destination resources. A properly configured CBR rule restricts all access to resources unless the request originates from {{site.data.keyword.atracker_full_notm}} or approved locations. 

Make sure you also have a service to service policy defined between {{site.data.keyword.atracker_full_notm}} and your destination resources. 
{: important}

To configure context-based restrictions, do the following:

1. Define a [network zone](/docs/account?topic=account-context-restrictions-create&interface=cli#network-zones-create-cli) that references {{site.data.keyword.atracker_full_notm}} from the service drop-down list. The **Locations** option is optional. If you do not specify a location, all  {{site.data.keyword.atracker_full_notm}} service locations are included. Here is an example to create a zone by using the CLI CBR plug-in:

   ```text
   ibmcloud cbr zone-create --name "Atracker-Zone-All-Regions" --description "Activity Tracker Event Routing For All regions" --service-ref service_name=atracker
   ...
   OK

   id                    1111b52afc14facafe797e34292b1001
   crn                   crn:v1:bluemix:public:context-based-restrictions:global:a/<account-id>::zone:1111b52afc14facafe797e34292b1001
   address_count         1
   excluded_count        0
   name                  Atracker-Zone-All-Regions
   account_id            <account-id>
   description           Activity Tracker Event Routing For All regions
   addresses             1 Service Reference
   excluded              No addresses
   href                  https://cbr.cloud.ibm.com/v1/zones/1111b52afc14facafe797e34292b1001
   ```
   {: screen}

2. Define one or more [network zones](/docs/account?topic=account-context-restrictions-create&interface=cli#network-zones-create-cli) that you might want to access resources from the UI, CLI or any other clients.

3. Create a [CBR rule](docs/account?topic=account-context-restrictions-create&interface=cli#context-restrictions-create-rules-cli) that can be scoped to the resource instance, or resource, you want the rule to protect, and select the network zones you defined in the previous steps. Here are 2 examples to define rules to protect 1 {{site.data.keyword.cos_full_notm}} bucket and 1 {{site.data.keyword.logs_full_notm}} instance:

   ```text
   ibmcloud cbr rule-create --description "Allow Atracker-Zone-All-Regions and Client-GreenZone to access the Log instance" --service-name logs --service-instance 44445555-a4f1-4f8a-a954-75f083c7e001 --zone-id "222220d595a54f650157aa5e2b26d002,1111b52afc14facafe797e34292b1001" --enforcement-mode "enabled"
   ...
   OK

   id                    666673cf9f5ec11f591bd62987358001
   crn                   crn:v1:bluemix:public:context-based-restrictions:global:a/<account-id>::rule:666673cf9f5ec11f591bd62987358001
   description           Allow Atracker-Zone-All-Regions and Client-GreenZone to access the Log instance
   enforcement_mode      enabled
   operations            1 API Type
   contexts              1 Context
   resources
                         serviceInstance   44445555-a4f1-4f8a-a954-75f083c7e001
                         serviceName       logs
   href                  https://cbr.cloud.ibm.com/v1/rules/666673cf9f5ec11f591bd62987358001
   ```
   {: screen}

   ```text
   ibmcloud cbr rule-create --description "Allow Atracker-Zone-All-Regions and Client-GreenZone to access the COS bucket" --resource-attributes "serviceName=cloud-object-storage,serviceInstance=66667777-dae3-4300-afde-7d5a70e88a83,resource=my-cos-bucket" --zone-id "222220d595a54f650157aa5e2b26d002,1111b52afc14facafe797e34292b1001" --enforcement-mode "enabled"
   ...
   OK

   id                    777773cf9f5ec11f591bd62987357001
   crn                   crn:v1:bluemix:public:context-based-restrictions:global:a/<account-id>::rule:777773cf9f5ec11f591bd62987357001
   description           Allow Atracker-Zone-All-Regions and Client-GreenZone to access the COS bucket
   enforcement_mode      enabled
   operations            1 API Type
   contexts              1 Context
   resources
                         resource          my-cos-bucket
                         serviceInstance   66667777-dae3-4300-afde-7d5a70e88a83
                         serviceName       cloud-object-storage
   href                  https://cbr.cloud.ibm.com/v1/rules/777773cf9f5ec11f591bd62987357001
   ```
   {: screen}

4. Create or validate the target that points to the destination resources. If your CBR rule is configured properly, a test event will be able to write to the destination and the target will be created or validated. If not, you will receive an *access forbidden* error instead. For example:
   
   ```text
   ibmcloud at target validate --target <target-uuid>
   OK
   Target
   Name:                    <target-name>
   ID:                      <target-uuid>
   CRN:                     crn:v1:bluemix:public:atracker:<region>:a/<account-id>::target:<target-uuid>
   Region:                  <region>
   Type:                    cloud_logs
   Cloud Logs Target CRN:   crn:v1:bluemix:public:logs:<region>:a/<account-id>:44445555-a4f1-4f8a-a954-75f083c7e001::
   Write Status:            success
   ```
   {: screen}


## Using context-based restrictions to protect the public API
{: #cbr-api-using}

As an account owner, you can limit access to the {{site.data.keyword.atracker_full_notm}} API from your account. A properly configured CBR rule restricts all access to the {{site.data.keyword.atracker_full_notm}} API from your account unless the request originates from the approved nework locations.

To configure context-based restrictions to protect the API, do the following:

1. Define one or more [network zones](/docs/account?topic=account-context-restrictions-whatis#network-zones-whatis) that might call the {{site.data.keyword.atracker_full_notm}} API from the UI, CLI or any other clients. You can define network zones from the {{site.data.keyword.cloud_notm}} UI or CLI. The following is an example of how to create a zone by using the CLI CBR plug-in:

   ```text
   % ibmcloud cbr zone-create --name "Atracker-Api-client-zone" --description "Network zone for ATracker CLI, UI or any other clients" --addresses 169.70.115.5,169.60.137.153
   ...
   OK

   id                    86e1776051c9b23a0b3c038b412eb08e
   crn                   crn:v1:bluemix:public:context-based-restrictions:global:a/<account-id>::zone:86e1776051c9b23a0b3c038b412eb08e
   address_count         2
   excluded_count        0
   name                  Atracker-Api-client-zone
   account_id            <account-id>
   description           Network zone for ATracker CLI, UI or any other clients
   addresses             2 IP Addresses
   excluded              No addresses
   href                  https://cbr.cloud.ibm.com/v1/zones/86e1776051c9b23a0b3c038b412eb08e
   ......
   ```
   {: screen}

2. Create a [CBR rule](/docs/account?topic=account-context-restrictions-whatis#rule-scope) to protect the {{site.data.keyword.atracker_full_notm}} API for your account using the network zones created in the previous step. You can create CBR rules from the {{site.data.keyword.cloud_notm}} UI or CLI. The following is an example of how to create such a rule by using CLI CBR plug-in:

   ```text
   % ibmcloud cbr rule-create --description "Allow Atracker-Api-client-zone to call ATracker API" --service-name atracker --zone-id 86e1776051c9b23a0b3c038b412eb08e --enforcement-mode enabled

   ...
   OK

   id                    5ee673cf9f5ec11f591bd6298741dbf1
   crn                   crn:v1:bluemix:public:context-based-restrictions:global:a/<account-id>::rule:5ee673cf9f5ec11f591bd6298741dbf1
   description           Allow Atracker-Api-client-zone to call ATracker API
   enforcement_mode      enabled
   operations            1 API Type
   contexts              1 Context
   resources
                         serviceName   atracker

   href                  https://cbr.cloud.ibm.com/v1/rules/5ee673cf9f5ec11f591bd6298741dbf1
   ......
   ```
   {: screen}

3. Verify that you have access to {{site.data.keyword.atracker_full_notm}} API. If your CBR rule is configured properly, your {{site.data.keyword.atracker_full_notm}} API call will be successful. If not, you will receive an *access forbidden* error instead.

   ```text
   % ibmcloud at target get --target 04c6e42c-9c61-4c5e-83ec-73a00f1655b7
   OK
   Target
   Name:                         my_target_name
   ID:                           04c6e42c-9c61-4c5e-83ec-73a00f1655b7
   CRN:                          crn:v1:bluemix:public:atracker:us-south:a/<account_id>::target:04c6e42c-9c61-4c5e-83ec-73a00f1655b7
   ......
   ```
   {: screen}

## Invoking public and private endpoints
{: #cbr-invoke}

{{site.data.keyword.atracker_full_notm}} API supports both public endpoints and private endpoints. Depending on where the API requests come from and the endpoint type, the addresses used in CBR zone definition could be different. The following table provides some example request origins and corresponding addresses used in the CBR zone definition. 

|Request Origin|Endpoint Type| Addresses in zone definition |
|---|---|---|
| {{site.data.keyword.deliverypipeline}} | public and private | [Toolchain service reference](/docs/ContinuousDelivery?topic=ContinuousDelivery-pipeline-subnet-ranges#toolchain-service-reference) |
| cluster on classic | public |  cluster [public primary subnet](/docs/containers?topic=containers-subnets#basics_subnets_public_vlan) |
| cluster on classic | private | cluster [private primary subnet](/docs/containers?topic=containers-subnets#basics_subnets_private_vlan) |
| cluster on VPC | public | VPC [public gateways](/docs/vpc?topic=vpc-about-public-gateways&interface=ui) |
| cluster on VPC | private |  VPC [Cloud Service Endpoint source addresses](/docs/vpc?topic=vpc-vpc-behind-the-curtain#cse-source-addresses) or  VPC CRN |
{: caption="Addresses to use based on origin and endpoint type" caption-side="bottom"}
