---

copyright:
  years:  2021, 2025
lastupdated: "2025-01-09"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Managing authorizations to grant access between services
{: #iam-service-auth}

Use {{site.data.keyword.iamlong}} (IAM) to create or remove an authorization that grants {{site.data.keyword.atracker_full_notm}} access to work with other services.
{: shortdesc}


## Authorizations
{: #iam-service-auth-1}

Many of the capabilities of IAM are focused on managing and enforcing user and application access to {{site.data.keyword.cloud_notm}} resources. However, you might encounter other scenarios in which you need to provide one service with access to a user's resource in another service. This type of access is called an authorization.

In a service to service (S2S) authorization:
- The source service is the service that is granted access to the target service.
- The roles that you select define the level of access for the source service.
- The target service is the service that you are granting permission to be accessed by the source service based on the roles that you assign.
- A source service can be in the same account where the authorization is created or in another account.
- The target service is always in the account where the authorization is created.

You can view whether the source service is located in the current account or another account by viewing the Source account column for the specific authorization on the [Authorizations](/iam/authorizations) page in the {{site.data.keyword.cloud}} console.{: tip}


For more information, see [Using authorizations to grant access between services](/docs/account?topic=account-serviceauth).


## Supported service to service authorizations
{: #iam-service-auth-2}

The following table lists the different S2S authorizations that you can configure when you use the {{site.data.keyword.atracker_full_notm}} service:

| S2S Authorization | Source service | Target service |
|-------------------|----------------|----------------|
| Authorize access to write data into a bucket | {{site.data.keyword.atracker_full_notm}} | {{site.data.keyword.cos_full_notm}} |
| Authorize access to send data to the {{site.data.keyword.messagehub_full}} service | {{site.data.keyword.atracker_full_notm}} | {{site.data.keyword.messagehub_full}} |
| Authorize access to send data to the {{site.data.keyword.logs_full_notm}} service | {{site.data.keyword.atracker_full_notm}} | {{site.data.keyword.logs_full_notm}} |
{: caption="S2S authorizations."}

Service to service authorizations are supported in the following use cases:
- {{site.data.keyword.atracker_full_notm}} and the target service are in the same account.
- {{site.data.keyword.atracker_full_notm}} and the target service are in different accounts.


## Permissions to manage authorizations
{: #iam-service-auth-permissions}

You must have access to the target service to manage authorization between services.

If you create an authorization between a service in another account and a target service in your current account, you need to have access only to the target resource. For the source account, you need only the account ID. 

The autorization that you define for the {{site.data.keyword.atracker_full_notm}} service requires that the ID that you use to create the S2S authorization has the following platform roles:

| Action              | Administrator | Operator | Editor | Viewer |
|---------------------|---------------|----------|--------|--------|
| View all authorizations that are configured in the account | ![Checkmark icon](../../icons/checkmark-icon.svg "checkmark") | | | |
| Create authorizations | ![Checkmark icon](../../icons/checkmark-icon.svg "checkmark") | | | |
| Delete authorizations | ![Checkmark icon](../../icons/checkmark-icon.svg "checkmark") | | | |
{: caption="Actions on the target service that are required to manage authorizations" caption-side="top"}

Users can only see authorizations that they configure in the account.

The autorization that you define for the {{site.data.keyword.atracker_full_notm}} service requires that the ID that you use to create the S2S authorization has the following service role per type of authorization:

| S2S Authorization | Service  |Service role |
|-------------------|----------|-------------|
| Authorize access to write data into a bucket | {{site.data.keyword.cos_full_notm}} | Object Writer |
| Authorize access to the {{site.data.keyword.messagehub_full}} service | {{site.data.keyword.messagehub_full}} | Writer |
| Authorize access to send data to the {{site.data.keyword.logs_full_notm}} service | {{site.data.keyword.logs_full}} | Sender |
{: caption="S2S authorizations."}


## Creating an authorization
{: #iam-service-auth-create-auth}


Choose one of the following options to create a S2S authorization:

- [Authorize access to write data into a bucket](/docs/atracker?topic=atracker-iam-service-auth-cos).
- [Authorize working with the {{site.data.keyword.messagehub_full}} service](/docs/atracker?topic=atracker-iam-service-auth-es).
- [Authorize working with the {{site.data.keyword.logs_full}} service](/docs/atracker?topic=atracker-iam-service-auth-logs).



## Removing an authorization
{: #iam-service-auth-remove-auth}


Choose one of the following options to remove a S2S authorization:
- [Remove a S2S authorization through the UI](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-remove-auth&interface=ui)
- [Remove a S2S authorization by using the CLI](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-remove-auth&interface=cli)
- [Remove a S2S authorization by using the API](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-remove-auth&interface=api)
- [Remove a S2S authorization by using terraform](/docs/cloud-logs?topic=cloud-logs-iam-service-auth-remove-auth&interface=terraform)


If the source service is removed from the account, any policies that are created by that service for its dependent services are deleted automatically. Similarly, if the dependent service is removed from the account, any access policies that are delegated to that service are also deleted.
{: note}
