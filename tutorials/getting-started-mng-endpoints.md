---

copyright:
  years:  2021, 2025
lastupdated: "2025-04-10"

keywords:

subcollection: atracker

content-type: tutorial
services: activity-tracker
account-plan: lite
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}


# Enforcing private endpoints to configure {{site.data.keyword.atracker_short}} resources
{: #getting-started-mng-endpoints}
{: toc-content-type="tutorial"}
{: toc-services="activity-tracker"}
{: toc-completion-time="1h"}

Use this tutorial to learn how to enforce the use of private endpoints to configure {{site.data.keyword.atracker_short}} resources in your account.
{: shortdesc}

You can use the {{site.data.keyword.atracker_short}} CLI or the {{site.data.keyword.atracker_short}} REST API to define the type of endpoints that are allowed to configure {{site.data.keyword.atracker_short}} resources in the account.


[![Step 1. Check that your account is VRF enabled.](../images/endpoint_s1.svg)](#getting-started-mng-endpoints-step1)
[![Step 2. Disable public endpoints.](../images/endpoint_s2.svg)](#getting-started-mng-endpoints-step2)
[![Step 3. Check you have access to private endpoints.](../images/endpoint_s3.svg)](#getting-started-mng-endpoints-step3)



## Prerequisites
{: #getting-started-mng-endpoints-prereqs}

- You need a user ID that is a member, or an owner of, an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Create an account](https://cloud.ibm.com/login){: external}.

- If you prefer to work with the command line, you must install the {{site.data.keyword.cloud_notm}} CLI. For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

- Your user ID needs **administrator platform permissions** to manage the {{site.data.keyword.atracker_full_notm}} service. Contact the account owner. The account owner can grant another user access to the account for the purposes of managing user access, and managing account resources. [Learn more](/docs/account?topic=account-userroles).


## Check your account is VRF enabled
{: #getting-started-mng-endpoints-step1}
{: step}

By default, public endpoints are enabled in your account. To allow the usage of private endpoints in your account, you must enable the account for virtual routing and forwarding (VRF).

- When using the classic infrastructure, you connect to resources in your account over the {{site.data.keyword.cloud_notm}} public network by default. You can enable virtual routing and forwarding (VRF) to move IP routing for your account and all of its resources into a separate routing table. If VRF is enabled, you can then enable {{site.data.keyword.cloud_notm}} service endpoints to connect directly to resources without using the public network. [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).

- Virtual Private Clouds (VPCs) are automatically enabled for virtual routing and forwarding (VRF). To enable service endpoints for your VPC, continue to [Enabling service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).


For example, to check if the account is VRF enabled, run the following command:

```text
ibmcloud account show
```
{: pre}


To enable private endpoints, run the following command:

```text
ibmcloud account update --service-endpoint-enable true
```
{: pre}




## Disable public endpoints in the account
{: #getting-started-mng-endpoints-step2}
{: step}

To disable public endpoints, run the following command:

```pre
ibmcloud atracker setting update --private-api-endpoint-only TRUE
```
{: codeblock}


## Check you have access to private endpoints
{: #getting-started-mng-endpoints-step3}
{: step}

After you disable public endpoints, you must configure {{site.data.keyword.atracker_short}} within the private network.

For example, to configure {{site.data.keyword.atracker_short}} in your account, you can provision a VPC VSI. Then, from a terminal, you can run cURL commands to create a target and a route.

Complete the following steps to provision a VPC VSI so that you can run cURL commands to create a target and a route in your account:

1. [Generate an ssh key](/docs/vpc?topic=vpc-ssh-keys).

2. [Create a VSI](/docs/vpc?topic=vpc-creating-virtual-servers) in your account.

3. [Connect to the VSI](/docs/vpc?topic=vpc-vsi_is_connecting_linux) from a terminal in your local environment.

4. After you ssh into the VSI, [install the IBM Cloud CLI](https://cloud.ibm.com/docs/cli?topic=cli-install-ibmcloud-cli). Run the following command:

    ```shell
    curl -fsSL https://clis.cloud.ibm.com/install/linux | sh
    ```
    {: pre}

You can run the following command to check that you can access the private endpoints:

```text
ping private.{region}.atracker.cloud.ibm.com
```
{: pre}

For example, you can run the following command to check access to the Dallas region:

```text
ping private.us-south.atracker.cloud.ibm.com
```
{: screen}
