---

copyright:
  years: 2019, 2024
lastupdated: "2024-01-18"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Managing access with IAM
{: #iam}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and control access to all cloud resources consistently in the {{site.data.keyword.cloud_notm}}. Access to {{site.data.keyword.atracker_full_notm}} service instances for users in your account is controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM).
{: shortdesc}

The access policy that you assign users in your account determines what actions a user can perform within the context of the service or specific instance that you select. The allowable actions are customized and defined by {{site.data.keyword.atracker_short}} as operations that are allowed to be performed on the service. An action is mapped to an IAM platform or service role that you can assign to a user.


## {{site.data.keyword.cloud_notm}} platform roles
{: #platform}

The following tables detail actions that are mapped to platform roles.

Platform roles enable users to perform tasks on service resources at the platform level, for example, assign user access for the service, create or delete instances, and bind instances to applications.

Review the following tables that outline what types of tasks each role allows for when you're configuring {{site.data.keyword.atracker_short}} in your account.

Use the following table to identify the **Account management** **{{site.data.keyword.atracker_short}}** platform role that you can grant a user in the {{site.data.keyword.cloud_notm}} to run any of the following platform actions:

| Platform role            | Description of actions |
|--------------------------|------------------------|
| Viewer                   | As a viewer, you can view {{site.data.keyword.atracker_short}} configuration resources such as routes and targets. |
| Operator                 | As an operator, you can view {{site.data.keyword.atracker_short}} configuration resources such as routes and targets. |
| Editor                   | As an editor, you can view, create, update, and delete {{site.data.keyword.atracker_short}} resources such as routes and targets. |
| Administrator            | As an administrator, you can view, create, update, and delete {{site.data.keyword.atracker_short}} resources. You can also assign access policies to manage {{site.data.keyword.atracker_short}} resources to other users in the account. |
{: caption="Table 1. IAM platform roles for {{site.data.keyword.atracker_short}}" caption-side="top"}
{: summary="Descriptions of the actions in the service that are permitted for the listed platform management role."}


## IAM actions by task
{: #iam_ater_bytask}

Review the available platform roles that are available, and the actions that are mapped to each to help you assign access.

For {{site.data.keyword.atracker_short}}, the IAM actions and Activity Tracker actions are the same.
{: note}


| Action | IAM and Activity Tracker action | Administrator | Editor | Operator | Viewer |
|--------|------------|---------------|--------|-----------|--------|
| Grant other account members access to configure {{site.data.keyword.atracker_short}} | `iam-am.policy.create` |![Checkmark icon](../../icons/checkmark-icon.svg) | | | |
| Revoke member access to configure {{site.data.keyword.atracker_short}} | `iam-am.policy.delete` | ![Checkmark icon](../../icons/checkmark-icon.svg) | | | |
| Modify member access to configure {{site.data.keyword.atracker_short}}  | `iam-am.policy.update` | ![Checkmark icon](../../icons/checkmark-icon.svg) | | | |
{: caption="Table 2. IAM platform roles for {{site.data.keyword.atracker_short}} access actions" caption-side="top"}


| Action | IAM and Activity Tracker action | Administrator | Editor | Operator | Viewer |
|--------|------------|---------------|--------|-----------|--------|
| View a target      | `atracker.target.read` |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) |
| List all targets   | `atracker.target.list` |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) |
| Create a target    | `atracker.target.create` |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) | | |
| Update a target    | `atracker.target.update` |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) | | |
| Delete a target    | `atracker.target.delete` |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) | | |
{: caption="Table 3. IAM platform roles for {{site.data.keyword.atracker_short}} target actions" caption-side="top"}

| Action | IAM and Activity Tracker | Administrator | Editor | Operator | Viewer |
|--------|------------|---------------|--------|-----------|--------|
| View a route | `atracker.route.read` |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) |
| List all routes | `atracker.route.list` |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) |
| Create a route | `atracker.route.create` |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) | | |
| Update a route | `atracker.route.update` |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) | | |
| Delete a route | `atracker.route.delete` |![Checkmark icon](../../icons/checkmark-icon.svg) |![Checkmark icon](../../icons/checkmark-icon.svg) | | |
{: caption="Table 4. IAM platform roles for {{site.data.keyword.atracker_short}} route actions" caption-side="top"}


| Action | IAM and Activity Tracker action | Administrator | Editor | Operator | Viewer |
|--------|------------|---------------|--------|-----------|--------|
| View configuration settings  | `atracker.setting.get` | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| Update configuration settings | `atracker.setting.update` | ![Checkmark icon](../../icons/checkmark-icon.svg) | | | |
{: caption="Table 5. IAM platform roles for {{site.data.keyword.atracker_short}} configuration actions" caption-side="top"}

## Assigning access to {{site.data.keyword.atracker_full_notm}}
{: #iam-assign-access-how}

For details on assigning access, see [Assigning access to {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-iam).

## How do I know which access policies are set for me?
{: #iam_accesspolicy}

You can see which access policies are set for you in the [{{site.data.keyword.cloud_notm}} UI](https://cloud.ibm.com/){: external} console.

1. Go to [Access IAM users](https://cloud.ibm.com/iam/users){: external}.
2. Click your name in the user table.
3. Click the **Access policies** tab to see your access policies.
4. Click the **Access groups** tab to see the access groups where you are a member. Check the policies for each group.
