---

copyright:
  years: 2019, 2023
lastupdated: "2021-08-09"

keywords:

subcollection: atracker


---

{{site.data.keyword.attribute-definition-list}}


# Using service endpoints to privately connect to {{site.data.keyword.atracker_full_notm}}
{: #service-endpoints}

To ensure that you have enhanced control and security over your data when you use {{site.data.keyword.atracker_full}}, you have the option of using private routes to {{site.data.keyword.cloud}} service endpoints. Private routes are not accessible or reachable over the internet. By using the {{site.data.keyword.cloud_notm}} private service endpoints feature, you can protect your data from threats from the public network and logically extend your private network.
{: shortdesc}

You can use private and public endpoints to configure {{site.data.keyword.atracker_full}} resources in your account.

You can connect to {{site.data.keyword.atracker_full_notm}} over a private network by using {{site.data.keyword.cloud_notm}} private service endpoints.

- When using the classic infrastructure, you connect to resources in your account over the {{site.data.keyword.cloud_notm}} public network by default. You can enable virtual routing and forwarding (VRF) to move IP routing for your account and all of its resources into a separate routing table. If VRF is enabled, you can then enable {{site.data.keyword.cloud_notm}} service endpoints to connect directly to resources without using the public network. [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).

- Virtual Private Clouds (VPCs) are automatically enabled for virtual routing and forwarding (VRF). To enable service endpoints for your VPC, continue to [Enabling service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).

## Before you begin
{: #prereq-service-endpoint}

Check if the account is VRF enabled by running the following command:

```text
ibmcloud account show
```
{: pre}

To enable private endpoints, run the following command:

```text
ibmcloud account update --service-endpoint-enable true
```
{: pre}



## Setting up service endpoints for {{site.data.keyword.atracker_full_notm}}
{: #endpoint-setup}

By default, private and public endpoints are enabled. For more information about supported endpoints, see [Endpoints](/docs/atracker?topic=atracker-endpoints).


## Disabling public service endpoints
{: #endpoint-disable}

You cannot disable private endpoints.
{: note}

You can disable public endpoints in your account for {{site.data.keyword.atracker_full_notm}} by using private or public endpoints.

For more information on how to disable a public endpoint, see [Enforcing private endpoints to configure {{site.data.keyword.atracker_short}} resources](/docs/atracker?topic=atracker-getting-started-mng-endpoints).

If public endpoints have been disabled, you can only enable public endpoints by using the private endpoint.
{: note}
