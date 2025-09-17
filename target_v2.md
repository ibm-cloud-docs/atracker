---

copyright:
  years:  2021, 2025
lastupdated: "2025-09-17"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Managing targets
{: #target_v2}

You can manage {{site.data.keyword.atracker_full}} targets in your account by using the {{site.data.keyword.atracker_short}} CLI, the {{site.data.keyword.atracker_short}} REST API, and Terraform scripts. A target is a resource where you can collect auditing events.
{: shortdesc}


## Understanding how targets work in your account
{: #target_v2_behavior}

Note the following information about targets:

* You can define up to 16 targets in each account. Each account can have up to 2 default targets.

* A target defines a resource where auditing events are collected. [Routes](/docs/atracker?topic=atracker-route_v2) define how auditing events that are generated in the account are routed to the targets that you configure.

* You can define a target in any of the supported locations where {{site.data.keyword.atracker_short}} is available. For more information, see [Locations](/docs/atracker?topic=atracker-regions).

* Targets are created within a region but are visible across regions. That is, all targets can be accessed by any {{site.data.keyword.atracker_full}} API endpoint.

* You can use private and public endpoints to manage targets. For more information about the list of `ENDPOINTS` that are available, see [Endpoints](/docs/atracker?topic=atracker-endpoints).

    * You can manage targets from the private network using an API endpoint with the following format: `https://private.REGION.atracker.cloud.ibm.com`

    * You can manage targets from the public network using an API endpoint with the following format: `https://REGION.atracker.cloud.ibm.com`

    * You can disable the public endpoints by updating the account settings. For more information, see [Enforcing private endpoints](/docs/atracker?topic=atracker-getting-started-mng-endpoints).


## Target types
{: #target_v2_types}

You can configure any of the following target types:

| Target                                                             | Type                     | Learn more |
|--------------------------------------------------------------------|--------------------------|------------|
| {{site.data.keyword.cos_full_notm}} (COS)                          | `cloud_object_storage`   | [Managing {{site.data.keyword.cos_full_notm}} (COS) targets](/docs/atracker?topic=atracker-target_v2_cos) |
| {{site.data.keyword.messagehub_full}} (Event Streams)              | `event_streams`          | [Managing {{site.data.keyword.messagehub_full}} (Event Streams) targets](/docs/atracker?topic=atracker-target_v2_ies) |
| {{site.data.keyword.logs_full_notm}}                          | `cloud_logs`   | [Managing {{site.data.keyword.logs_full_notm}} targets](/docs/atracker?topic=atracker-target_v2_icl) |
{: caption="List of targets" caption-side="top"}



## IAM Access
{: #target_v2_iam}

You must grant users IAM permissions to manage targets. For more information, see [Assign access to resources](/docs/account?topic=account-assign-access-resources).

When you define a policy, you can indicate the scope of the permissions. You can choose from granting permissions for a specific region or for the entire account.

If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned.
{: important}

Users with regional scope will be limited to access targets in their authorized region.
{: note}

| IAM action               | IAM Policy scope  | IAM Roles                          | Description         |
| ------------------------ | ----------------- | ---------------------------------- | -------------- |
| `atracker.target.read`   | Region         | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | Read (view) information about a target |
| `atracker.target.create` | Region         | `Administrator`  \n `Editor`                             | Create a target |
| `atracker.target.update` | Region         | `Administrator`  \n `Editor`                             | Update a target |
| `atracker.target.delete` | Region         | `Administrator`  \n `Editor`                             | Delete a target |
| `atracker.target.list`   | Account        | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | List all targets |
{: caption="Required IAM roles}


## Authentication options
{: #target_v2_auth}

To route events to a target, check the options that you can use to authenticate for that target type.

| Target                   | Service to Service (S2S) authentication | API key    |
|--------------------------|-----------------------------------------|------------|
| `cloud_object_storage`   | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") |
| `event_streams`          | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") |
| `cloud_logs`   | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") | |
{: caption="Authentication options by target type" caption-side="top"}


## Validating targets
{: #target_v2_validate}

When you validate a target, you check that the credentials that are configured for a target are valid. These credentials are used by {{site.data.keyword.atracker_short}} to authenticate with the destination target.

You can validate a target by using the {{site.data.keyword.metrics_router_full_notm}} CLI, the {{site.data.keyword.metrics_router_full_notm}} REST API, and Terraform scripts.

| Target type | CLI | API |
|-------------|-----|-----|
| `cloud-object-storage` | [Validate via CLI](/docs/atracker?topic=atracker-target_v2_cos&interface=cli#target-validate-cli-cos) | [Validate via API](/docs/atracker?topic=atracker-target_v2_cos&interface=api#target-validate-api-cos) |
| `event_streams` | [Validate via CLI](/docs/atracker?topic=atracker-target_v2_ies&interface=cli#target-validate-cli-ies) | [Validate via API](/docs/atracker?topic=atracker-target_v2_ies&interface=api#target-validate-api-ies) |
| `cloud_logs` | [Validate via CLI](/docs/atracker?topic=atracker-target_v2_icl&interface=cli#target-validate-cli-icl) | [Validate via API](/docs/atracker?topic=atracker-target_v2_icl&interface=api#target-validate-api-icl) |
{: caption="Validating options by target type" caption-side="top"}



## CLI prerequisites
{: #target_v2_cli}
{: cli}

Before you use the CLI to manage targets, complete the following steps:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-atracker-cli-config).


## CLI commands
{: #target_v2_cli_cmd}
{: cli}

The following table lists the actions that you can run to manage targets:

| Action                     | Command                             |
|----------------------------|-------------------------------------|
| Create a target            | `ibmcloud atracker target create`   |
| Update a target            | `ibmcloud atracker target update`   |
| Delete a target            | `ibmcloud atracker target delete`   |
| Read a target              | `ibmcloud atracker target get`      |
| List all targets           | `ibmcloud atracker target ls`       |
| Validate a target          | `ibmcloud atracker target validate` |
{: caption="Target actions by using the {{site.data.keyword.atracker_full_notm}}Event Routing CLI" caption-side="top"}


For more information, see [{{site.data.keyword.atracker_full_notm}} V2 CLI](/docs/atracker?topic=atracker-atracker-v2-cli).



## API targets and actions
{: #target_v2_api}
{: api}

To make API calls to manage targets, complete the following steps:
1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/atracker?topic=atracker-retrieve-iam-token).
2. Identify the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints).


The following table lists the actions that you can run to manage targets:

| Action                     | REST API Method  | API_URL                                          |
|----------------------------|------------------|--------------------------------------------------|
| Create a target            | `POST`           | `<ENDPOINT>/api/v2/targets`              |
| Update a target            | `PUT`            | `<ENDPOINT>/api/v2/targets/<TARGET_ID>`  |
| Delete a target            | `DELETE`         | `<ENDPOINT>/api/v2/targets/<TARGET_ID>`  |
| Read a target              | `GET`            | `<ENDPOINT>/api/v2/targets/<TARGET_ID>`  |
| List all targets           | `GET`            | `<ENDPOINT>/api/v2/targets`             |
| Validate a target          | `POST`           | `<ENDPOINT>/api/v2/targets/{id}/validate` |
{: caption="Target actions by using the {{site.data.keyword.atracker_full_notm}} REST API" caption-side="top"}


For more information, see [{{site.data.keyword.atracker_full_notm}} V2 API](https://{DomainName}/apidocs/atracker).


## HTTP response codes
{: #target_v2_api_rc}
{: api}

When you use the {{site.data.keyword.atracker_full_notm}} REST API, you can get standard HTTP response codes to indicate whether a method completed successfully.

- A 200 response always indicates success.
- A 4xx response indicates a failure.
- A 5xx response usually indicates an internal system error.

See the following table for some HTTP response codes:

| Status code | Status | Description |
|-------------|--------|-------------|
| `200` |	OK | The request was successful. |
| `201` |	OK | The request was successful. A resource is created. |
| `400` | Bad Request |	The request was unsuccessful. You might be missing a parameter that is required. |
| `401` |	Unauthorized | The IAM token that is used in the API request is invalid or expired. |
| `403` |	Forbidden | The operation is forbidden due to insufficient permissions. |
| `404` | Not Found |	The requested resource doesn't exist or is already deleted. |
| `429` |	Too Many Requests |	Too many requests hit the API too quickly. |
| `500` |	Internal Server Error |	Something went wrong in {{site.data.keyword.atracker_full_notm}} processing. |
{: caption="List of HTTP response codes" caption-side="top"}


## Next
{: #target_v2_next}

Choose 1 of the following options to configure a target in your account:
- [Managing {{site.data.keyword.cos_full_notm}} (COS) targets](/docs/atracker?topic=atracker-target_v2_cos).
- [Managing {{site.data.keyword.messagehub_full}} targets](/docs/atracker?topic=atracker-target_v2_ies)
- [Managing {{site.data.keyword.logs_full_notm}} targets](/docs/atracker?topic=atracker-target_v2_icl)


## Managing targets using the UI
{: #target-v2-ui}
{: ui}

You can manage your {{site.data.keyword.atracker_full_notm}} targets, routes, and settings using the IBM Console.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.
3. Select **Activity Tracker**.
4. Select **Routing**.

For more information, see [Managing {{site.data.keyword.logs_full_notm}} targets](/docs/atracker?topic=atracker-target_v2_icl&interface=ui).
