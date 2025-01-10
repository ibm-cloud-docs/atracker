---

copyright:
  years:  2021, 2025
lastupdated: "2025-01-10"

keywords:

subcollection: atracker

content-type: tutorial
services: atracker
account-plan: lite
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}


# Configuring an {{site.data.keyword.logs_full_notm}} instance as a target
{: #getting-started-target-cloud-logs}
{: toc-content-type="tutorial"}
{: toc-services="atracker"}
{: toc-completion-time="1h"}


A target is an {{site.data.keyword.cloud_notm}} resource where you can collect auditing events. Use this tutorial to learn how to configure an {{site.data.keyword.logs_full_notm}} target in the account.
{: shortdesc}

## Scenarios
{: #getting-started-target-cloud-logs-scenarios}

You can define a {{site.data.keyword.logs_full_notm}} instance as a target in any of the following situations:
- You want to collect and store auditing events in {{site.data.keyword.logs_full_notm}}. You can have the instance in the account that generates the events or in a different account from the one that generates auditing events.


## Prerequisites
{: #getting-started-target-cloud-logs-prereqs}

- You need a user ID that is a member, or an owner of, an {{site.data.keyword.cloud_notm}} account. To get an {{site.data.keyword.cloud_notm}} user ID, go to: [Create an account](https://cloud.ibm.com/login){: external}.

- Learn about {{site.data.keyword.atracker_short}}. For more information, see [About](/docs/atracker?topic=atracker-atracker-resources).

- Install the {{site.data.keyword.cloud_notm}} CLI. For more information, see [Installing the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

- Install the latest {{site.data.keyword.atracker_short}} CLI V2 plugin in your local system. See [Installing the {{site.data.keyword.atracker_short}} CLI](/docs/atracker?topic=atracker-atracker-cli-config&interface=cli).

- Every user that manages the {{site.data.keyword.atracker_short}} configuration in your account must be assigned an access policy. The policy determines what actions the user can perform. The allowable actions are customized and defined by {{site.data.keyword.atracker_short}} as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles. [Learn more](/docs/atracker?topic=atracker-iam).

    Your user ID needs **administrator platform permissions** to manage the {{site.data.keyword.atracker_full_notm}} service. Contact the account owner. The account owner can grant another user access to the account for the purposes of managing user access, and managing account resources. [Learn more](/docs/account?topic=account-userroles).

## Provision a {{site.data.keyword.logs_full_notm}} instance
{: #getting-started-target-cloud-logs-step2}
{: step}

Provision an {{site.data.keyword.logs_full_notm}} instance. See [Provisioning an instance](/docs/cloud-logs?topic=cloud-logs-instance-provision&interface=ui).

## Configure service-to-service authorization
{: #getting-started-target-cloud-logs-step3}
{: step}

Configure service-to-service authorization to your {{site.data.keyword.logs_full_notm}} instance. For more information, see [Creating a S2S authorization to grant access to the {{site.data.keyword.logs_full_notm}} service](/docs/atracker?topic=atracker-iam-service-auth-logs).


## Create a target
{: #getting-started-target-cloud-logs-step4}
{: step}

To create an {{site.data.keyword.logs_full_notm}} target from the Observability dashboard in the {{site.data.keyword.cloud_notm}}, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in, the {{site.data.keyword.cloud_notm}} UI opens.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Activity Tracker** &gt; **Routing**.

4. Click **Create**.

5. Choose {{site.data.keyword.logs_full_notm}} for the type.

6. If you have not yet configured a service-to-service authorization policy, you will see: *Service authorization required*.

    To grant access to Activity Tracker Event Routing to send to any {{site.data.keyword.logs_full_notm}} instance in your account, select **Authorize now**.

7. Select the instance of {{site.data.keyword.logs_full_notm}} under **Choose the destination**.

8. Provide the name of the target for *Target name*.

9. Select **Create target**.

## Create a route
{: #getting-started-target-cloud-logs-step5}
{: step}

Define 1 or more routes in the account. For more information, see [Configuring a route](/docs/atracker?topic=atracker-route_v2&interface=cli#route-create-cli).

When you configure a route, you associate a target with a route and define which type of auditing events are routed. The route defines the rules that determine where auditing events are routed in your account. For example, you can define a route that routes auditing events from 2 different regions, and also routes global events.


You can collect [global events](/docs/atracker?topic=atracker-event_types#event_types_global) and [location-based events](/docs/atracker?topic=atracker-event_types#event_types_location).
- Global events report on activity in your account that relate to data and resources that are generally synchronized across all regions.
- Location-based events report on activity in your account that is generated by IBM Cloud services that are hosted within an IBM data center location, such as US-South or US-East.


## Next
{: #getting-started-target-cloud-logs-next}
{: step}

Launch the {{site.data.keyword.logs_full_notm}} instance UI. For more information, see [Launching the UI](/docs/cloud-logs?topic=cloud-logs-instance-launch). Then, create some views to monitor your data. For more information, see [Managing customer views](/docs/cloud-logs?topic=cloud-logs-custom_views).
