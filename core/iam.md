---

copyright:
  years: 2019, 2023
lastupdated: "2022-11-11"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Managing access with IAM
{: #iam}

{{site.data.keyword.iamlong}} (IAM) enables you to securely authenticate users and control access to all cloud resources consistently in the {{site.data.keyword.cloud_notm}}. Access to {{site.data.keyword.at_full_notm}} service instances for users in your account is controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM).
{: shortdesc}

The access policy that you assign users in your account determines what actions a user can perform within the context of the service or specific instance that you select. The allowable actions are customized and defined by {{site.data.keyword.atracker_short}} as operations that are allowed to be performed on the service. An action is mapped to an IAM platform or service role that you can assign to a user.

For more information about the steps to assign IAM access, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).
- When you assign policies to users by using a CLI command or API call, use `atracker`.
- When you assign policies to users through the UI, use `Activity Tracking`.

**To organize a set of users and service IDs into a single entity that makes it easy for you to manage IAM permissions, use *access groups*.** You can assign a single policy to the group instead of assigning the same access multiple times per individual user or service ID.
{: tip}


## Managing access by using access groups
{: #groups}

To manage access or assign new access for users by using access groups, you must be the account owner, administrator, or editor on all Identity and Access enabled services in the account, or the assigned administrator or editor for the IAM Access Groups Service.

Choose any of the following actions to manage access groups in the {{site.data.keyword.cloud_notm}}:

* [Creating an access group](/docs/account?topic=account-groups#create_ag).
* [Assigning access to a group](/docs/account?topic=account-groups#access_ag).


## Managing access by assigning policies directly to users
{: #users}

To manage access or assign new access for users by using IAM policies, you must be the account owner, administrator on all services in the account, or an administrator for the particular service or service instance.

Choose any of the following actions to manage IAM policies in the {{site.data.keyword.cloud_notm}}:

* To grant permissions to a user, see [Assigning access](/docs/account?topic=account-assign-access-resources#assign_new_access).
* To revoke permissions, see [Removing access](/docs/account?topic=account-assign-access-resources#removing_access).
* To review a user's permissions, see [Reviewing your assigned access](/docs/account?topic=account-assign-access-resources#review_your_access).

## Managing access through trusted profiles
{: #iam-profiles}

[Trusted profiles](/docs/account?topic=account-identity-overview#trustedprofiles-bestpract) are supported.

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
| Set endpoint properties `[V1]` | `atracker.endpoint.set` | ![Checkmark icon](../../icons/checkmark-icon.svg) | | |  |
| View endpoint properties `[V1]` | `atracker.endpoint.get` | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
{: caption="Table 5. IAM platform roles for {{site.data.keyword.atracker_short}} endpoint actions" caption-side="top"}


| Action | IAM and Activity Tracker action | Administrator | Editor | Operator | Viewer |
|--------|------------|---------------|--------|-----------|--------|
| View configuration settings `[V2]` | `atracker.setting.get` | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| Update configuration settings `[V2]` | `atracker.setting.update` | ![Checkmark icon](../../icons/checkmark-icon.svg) | | | |
{: caption="Table 6. IAM platform roles for {{site.data.keyword.atracker_short}} configuration actions" caption-side="top"}

| Action | IAM and Activity Tracker action | Administrator | Editor | Operator | Viewer |
|--------|------------|---------------|--------|-----------|--------|
| Start migration `[V2]` | `atracker.migration.post` | ![Checkmark icon](../../icons/checkmark-icon.svg) | | | |
| View migration status `[V2]` | `atracker.migration.get` | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
{: caption="Table 7. IAM platform roles for {{site.data.keyword.atracker_short}} migration actions" caption-side="top"}

`[V2]` is only applicable once you have [migrated to the V2 configuration.](/docs/activity-tracker?topic=activity-tracker-migration)  `[V1]` is only applicable to the V1 configuration and is unavailable after you migrate to the V2 configuration. All others are applicable to both configurations.
{: note}




## How do I know which access policies are set for me?
{: #iam_accesspolicy}

You can see which access policies are set for you in the [{{site.data.keyword.cloud_notm}} UI](https://cloud.ibm.com/){: external} console.

1. Go to [Access IAM users](https://cloud.ibm.com/iam/users){: external}.
2. Click your name in the user table.
3. Click the **Access policies** tab to see your access policies.
4. Click the **Access groups** tab to see the access groups where you are a member. Check the policies for each group.
