---

copyright:
  years: 2021, 2025
lastupdated: "2025-01-31"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.atracker_short}}
{: #vpe-connection}

{{site.data.keyword.cloud}} Virtual Private Endpoints (VPE) for VPC enables you to connect to {{site.data.keyword.atracker_short}} from your VPC network by using the IP addresses of your choosing, allocated from a subnet within your VPC.
{: shortdesc}

VPEs are virtual IP interfaces that are bound to an endpoint gateway created on a per service, or service instance, basis (depending on the service operation model). The endpoint gateway is a virtualized function that scales horizontally, is redundant and highly available, and spans all availability zones of your VPC. Endpoint gateways enable communications from virtual server instances within your VPC and the {{site.data.keyword.cloud}} service on the private backbone. VPE for VPC gives you the experience of controlling all the private addressing within your cloud. For more information, see [About virtual private endpoint gateways](/docs/vpc?topic=vpc-about-vpe).


## Before you begin
{: #prereq-service-endpoint}

Before you target a virtual private endpoint for {{site.data.keyword.atracker_short}} you must complete the following tasks.

* Ensure that a [Virtual Private Cloud is created](/docs/vpc?topic=vpc-getting-started).
* Make a plan for your [virtual private endpoints](/docs/vpc?topic=vpc-planning-considerations).
* Ensure that [correct access controls](/docs/vpc?topic=vpc-configure-acls-sgs-endpoint-gateways) are set for your virtual private endpoint.
* Understand the [limitations](/docs/vpc?topic=vpc-limitations-vpe) of having a virtual private endpoint.
* Understand how to [view details](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway) about a virtual private endpoint.

## Setting up a VPE for {{site.data.keyword.atracker_short}}
{: #endpoint-setup}

When you create a VPE gateway by using the CLI or API, you must specify the [Cloud Resource Name (CRN)](/docs/account?topic=account-crn) of the region in which you want connect to {{site.data.keyword.atracker_short}}. Review the following table for the available regions and CRNs to use to create your VPE gateway.


| Region | Cloud Resource Name (CRN) |
|-----------------|-----------------|
| `au-syd` | `crn:v1:bluemix:public:atracker:au-syd:::endpoint:private.au-syd.atracker.cloud.ibm.com` |
| `br-sao` | `crn:v1:bluemix:public:atracker:br-sao:::endpoint:private.br-sao.atracker.cloud.ibm.com` |
| `ca-tor` | `crn:v1:bluemix:public:atracker:ca-tor:::endpoint:private.ca-tor.atracker.cloud.ibm.com` |
| `eu-de` | `crn:v1:bluemix:public:atracker:eu-de:::endpoint:private.eu-de.atracker.cloud.ibm.com` |
| `eu-es` | `crn:v1:bluemix:public:atracker:eu-es:::endpoint:private.eu-es.atracker.cloud.ibm.com` |
| `eu-gb` | `crn:v1:bluemix:public:atracker:eu-gb:::endpoint:private.eu-gb.atracker.cloud.ibm.com` |
| `jp-osa` | `crn:v1:bluemix:public:atracker:jp-osa:::endpoint:private.jp-osa.atracker.cloud.ibm.com` |
| `jp-tok` | `crn:v1:bluemix:public:atracker:jp-tok:::endpoint:private.jp-tok.atracker.cloud.ibm.com` |
| `us-east` | `crn:v1:bluemix:public:atracker:us-east:::endpoint:private.us-east.atracker.cloud.ibm.com` |
| `us-south` | `crn:v1:bluemix:public:atracker:us-south:::endpoint:private.us-south.atracker.cloud.ibm.com` |
{: caption="Region availability and Cloud Resource Names for connecting {{site.data.keyword.atracker_short}} over {{site.data.keyword.cloud_notm}} private networks" caption-side="bottom"}


### Configuring an endpoint gateway
{: #endpoint-gateway-servicename}

To configure a virtual private endpoint gateway, follow these steps:

1. List the available services, including {{site.data.keyword.cloud_notm}} infrastructure services available (by default) for all VPC users.
1. [Create an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway) for {{site.data.keyword.atracker_short}} that you want to be privately available to the VPC.
1. [Bind a reserved IP address](/docs/vpc?topic=vpc-bind-unbind-reserved-ip) to the endpoint gateway.
1. View the created VPE gateways associated with {{site.data.keyword.atracker_short}}. For more information, see [Viewing details of an endpoint gateway](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway).

Now your virtual server instances in the VPC can access your {{site.data.keyword.atracker_short}} instance privately through it.

## Using your VPE for {{site.data.keyword.atracker_short}}
{: #using-servicename-vpe}

After you create an endpoint gateway for {{site.data.keyword.atracker_short}}, you can use the VPE with the VPC API.

### Using the VPE with the VPC API
{: #vpe-api}

After creating an endpoint gateway for the {{site.data.keyword.atracker_short}} service, use the service endpoints FQDN `private.<REGION>.atracker.cloud.ibm.com` in the URL to access the service. For example:

```sh
curl https://private.au-syd.atracker.cloud.ibm.com/api/v2/targets' -H "Authorization: Bearer $iam_token"
```
{: pre}
