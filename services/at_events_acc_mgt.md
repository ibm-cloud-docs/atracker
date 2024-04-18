---

copyright:
  years: 2019, 2024
lastupdated: "2024-01-18"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Auditing events for account management
{: #at_events_acc_mgt}

As a security officer, auditor, or manager, you can use the {{site.data.keyword.at_full_notm}} service to track how users and applications interact with an {{site.data.keyword.cloud}} account.
{: shortdesc}

The {{site.data.keyword.at_full_notm}} service records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. To get started, see [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).



## Events for managing accounts
{: #at_events_acc_mgt_account}

The following table lists the actions that generate an event:

| Action                               | Description |
|--------------------------------------|-------------|
| `billing.account.create`             | An event is generated when you create an account after the account ID is assigned to the account. |
| `billing.account.update`             | An event is generated when you update information about the account.  |
| `billing.account.active`             | An event is generated when you verify the account, that is, an event is generated when the account becomes active. |
| `billing.account-subscription.create` | An event is generated when you create a [Subscription account](/docs/account?topic=account-accounts#subscription-account). |
{: caption="Table 1. Actions that generate account management events" caption-side="top"}


## Events for managing account usage reports
{: #at_events_acc_mgt_account_reporst}

These events are generated when a user looks at usage information in the account. For example, the user can look at usage data through the **Manage** &gt; **Billing and usage** &gt; **Usage** section, or request an export of the data. Also, users can request usage information through the CLI or by making direct [API calls](/apidocs/metering-reporting#introduction).


### Events for managing single account usage reports
{: #at_events_acc_mgt_account_reporst_std}

The following table lists the actions that generate an event:

| Action                                               | Description |
|------------------------------------------------------|-------------|
| `billing.account-summary.read`                       | An event is generated when a user views the account level summary usage page that is displayed by default. |
| `billing.account-summary.download`                   | An event is generated when a user requests a **summary** export of the data in csv format from the account level summary usage page. |
| `billing.account-usage-report.read`                  | An event is generated when a user views the usage data that is displayed after the user configures a time frame, a resource group, or both in the default account level summary usage page. This event is also generated when a user views the instances usage data page. |
| `billing.account-instances-usage-report.download`    | An event is generated when a user requests an **instances** export of the data in csv format from the account level summary usage page. |
{: caption="Table 2. Actions that generate account management events" caption-side="top"}


### Events for managing enterprise usage reports
{: #at_events_acc_mgt_reporst_enterprise}

The following table lists the actions that generate an event:

| Action                                               | Description |
|------------------------------------------------------|-------------|
| `billing.enterprise-usage-report.read`               | An event is generated when a user views the enterprise account level summary usage page that is displayed by default. |
| `billing.enterprise-usage-report.download`          | An event is generated when a user requests a **summary** export of the data in csv format from the enterprise account level summary usage page.  |
| `billing.enterprise-instances-usage-report.download` | An event is generated when a user requests an **instances** export of the data in csv format from the enterprise account level summary usage page. |
{: caption="Table 3. Actions that generate account management events" caption-side="top"}

## Events for managing catalogs
{: #at_events_catalog_management}

The following tables list the actions that generate an event:

### Events for managing private catalogs
{: #at_events_catalog_1}

| Action                                           | Description                                                           |
|--------------------------------------------------|-----------------------------------------------------------------------|
| `globalcatalog-collection.instance.read`           | An event is generated when you view a catalog.            |
| `globalcatalog-collection.instance.update`         | An event is generated when you update a catalog.          |
| `globalcatalog-collection.instances.list`           | An event is generated when you get a list of the catalogs in an account.           |
{: caption="Table 4. Actions that generate catalog management events" caption-side="top"}

### Events for managing products in a private catalog
{: #at_events_catalog_2}

| Action                                           | Description                                                           |
|--------------------------------------------------|-----------------------------------------------------------------------|
| `globalcatalog-collection.offerings.list`         |  An event is generated when you get a list of the products in a catalog.          |
| `globalcatalog-collection.offering.read`           | An event is generated when you view a product in a catalog.            |
| `globalcatalog-collection.offering.create`         | An event is generated when you create a product.          |
| `globalcatalog-collection.offering.update`         | An event is generated when you update a product.          |
| `globalcatalog-collection.offering.delete`         | An event is generated when you delete a product.          |
{: caption="Table 5. Actions that generate events for products in a private catalog" caption-side="top"}

### Events for managing catalog settings at the account level
{: #at_events_catalog_5}

| Action                                           | Description                                                           |
|--------------------------------------------------|-----------------------------------------------------------------------|
| `globalcatalog-collection.account-settings.read`   | An event is generated when you view the account settings.   |
| `globalcatalog-collection.account-settings.update` | An event is generated when you update the account settings. |
{: caption="Table 6. Actions that generate events related to catalog management settings" caption-side="top"}

### Events for managing catalog settings in enterprise accounts
{: #at_events_catalog_4}

| Action                                           | Description                                                           |
|--------------------------------------------------|-----------------------------------------------------------------------|
| `globalcatalog-collection.enterprise-settings.read` | An event is generated when you view the enterprise settings. |
| `globalcatalog-collection.enterprise-settings.update` | An event is generated when you update the enterprise settings. |
| `globalcatalog-collection.enterprise-settings.list` | An event is generated when you get a list of the enterprises in an account and their corresponding settings. |
{: caption="Table 7. Actions that generate events related to catalog management settings in enterprise accounts" caption-side="top"}

### Events for managing software licenses and entitlements
{: #at_events_catalog_entitlement}

The following table lists the actions that generate an event:

| Action                                 | Description |
|----------------------------------------|---------|
| `entitlement.entitlement.create`       | An event is generated when an initiator binds a license to an account. |
| `entitlement.entitlement.delete`       | An event is generated when an initiator deletes an entitlement. |
| `entitlement.entitlement.delete_purge` | An event is generated when an initiator purges an entitlement. |
| `entitlement.entitlement.update`       | An event is generated when an initiator updates an entitlement. |
| `entitlement.entitlement.check`        | An event is generated when an initiator uses an entitlement to pull an image from the governed IBM Container Registry. |
| `entitlement.entitlement.invalidate`   | An event is generated when an entitlement's license is not valid anymore. |
{: caption="Table 8. Actions that generate events related to licenses and entitlements" caption-side="top"}

## Events for managing IAM account settings
{: #at_events_acc_mgt_acc_iam}


**Change to Activity Tracker events that report IAM account setting changes** : With immediate effect, you can track changes to IAM account settings by monitoring the `iam-identity.accountsettings.update` event. This event is now generated by the IAM Identity service. Next time you change an IAM configuration setting, you will get an event with action `iam-identity.accountsettings.migrate` that informs you that IAM account settings are reported by the IAM Identity service in your account. If you monitor changes to IAM account settings, you might need to migrate your resources to monitor `iam-identity.accountsettings.update` events.
{: important}

The following table lists the actions that are generated when an account setting that is controlled from the **Manage** &gt; **Access IAM** &gt; **Settings** dashboard is modified:

| Action                                     | Description |
|--------------------------------------------|-------------|
| `iam-identity.accountsettings.update`      | An event is generated when an initiator modifies 1 or more of the following account settings: `Multifactor authentication (MFA)`, `Restrict API key creation`, `Restrict service ID creation`, and `Restrict IP address access`. |
| `iam-groups.account-settings.update` | An event is generated when an initiator modifies the account setting `Public access group`. |
| `billing.account-traits.update`      | An event is generated when an initiator modifies the account setting `Restrict user list visibility`. |
{: caption="Table 9. Actions that generate events when the account settings are changed" caption-side="top"}


The following table lists the `requestData` fields that report the configuration changes:

| Action                                                         | Description |
|----------------------------------------------------------------|-------------|
| `requestData.public_access_enabled`                            | Reports the boolean value that is set when the `Public access group` setting is modified. |
| `requestData.request_body.old_mfa_traits`                      | Reports the original value for the `Multifactor authentication (MFA)` setting. Valid values are `NONE`, `TOTP`, `TOTP4ALL`, `LEVEL1`, `LEVEL2`, `LEVEL3`   \n  \n This field is set to `NONE` when MFA is not enabled in the account, and all users log in by using a standard ID and password.   \n  \n This field is set to `TOTP` when the account requires MFA for non-federated users only users with an IBMid. Users are required an ID, password, and a time-based one-time passcode to log in.   \n  \n This field is set to `TOTP4ALL` when the account requires MFA for all users with an IBMid.   \n  \n This field is set to `LEVEL1` to enable MFA for all users (IBMid & supported IdPs) when you choose the method `email-based MFA`. Users must authenticate by using a security passcode that is sent via email.     \n  \n This field is set to `LEVEL2` to enable MFA for all users (IBMid & supported IdPs) when you choose the method `TOTP MFA`. Users authenticate by using a time-based one-time passcode (TOTP) that uses the current time of day as an authentication factor.   \n  \n This field is set to `LEVEL3` to enable MFA for all users (IBMid & supported IdPs) when you choose the method `U2F MFA`. Users authenticate by using a hardware security key that generates a six-digit numerical code. |
| `requestData.request_body.new_mfa_traits`                      | Reports the new value for the `Multifactor authentication (MFA)` setting. |
| `requestData.request_body.old_restrict_create_platform_apikey` | Reports the original value for the `Restrict API key creation` setting.   \n Valid values: `NOT_RESTRICTED` and `RESTRICTED` |
| `requestData.request_body.new_restrict_create_platform_apikey` | Reports the new value for the `Restrict API key creation` setting.   \n Valid values: `NOT_RESTRICTED` and `RESTRICTED` |
| `requestData.request_body.old_restrict_create_service_id`      | Reports the original value for the `Restrict service ID creation` setting.   \n Valid values: `NOT_RESTRICTED` and `RESTRICTED` |
| `requestData.request_body.new_restrict_create_service_id`      | Reports the new value for the `Restrict service ID creation` setting.   \n Valid values: `NOT_RESTRICTED` and `RESTRICTED` |
| `requestData.request_body.old_allowed_ip_addresses`            | Reports the original value for the `Restrict IP address access` setting.   \n Valid values: `NOT_RESTRICTED` and `RESTRICTED` |
| `requestData.request_body.new_allowed_ip_addresses`            | Reports the new value for the `Restrict IP address access` setting.   \n Valid values: `NOT_RESTRICTED` and `RESTRICTED` |
| `requestData.team_directory_enabled`                           | Reports the boolean value that is set when the `Restrict user list visibility` setting is modified. |
{: caption="Table 10. Actions that generate events when the account settings are changed" caption-side="top"}


The following table lists the `deprecated` actions that generate an event when an account setting that is controlled from the **Manage** &gt; **Access IAM** &gt; **Settings** dashboard is modified:

| Action                               | Description |
|--------------------------------------|-------------|
| `billing.account-traits.update`      | An event is generated when an account setting is modified. |
| `billing.account-mfa.set-on`         | An event is generated when the `Account Login` setting sets on multifactor authentication in the account. |
| `billing.account-mfa.set-off`        | An event is generated when the `Account Login` setting sets off multifactor authentication in the account. |
{: caption="Table 11. Actions that generate events when the account settings are changed" caption-side="top"}

## Events for managing organizations
{: #at_events_acc_mgt_org}

The following table lists the actions that generate an event:

| Action                               | Description |
|--------------------------------------|-------------|
| `billing.account-org.create`         | An event is generated when you add an organization to the account. |
{: caption="Table 12. Actions that generate events" caption-side="top"}

## Events for managing software instances
{: #at_events_sw_instance}

The following table lists the actions that generate an event for software instances:

| Action                                           | Description                                                           |
|--------------------------------------------------|-----------------------------------------------------------------------|
| `globalcatalog-instance.offering-instance.create` | An event is generated when you create a software instance. |
| `globalcatalog-instance.offering-instance.delete` | An event is generated when you delete a software instance. |
| `globalcatalog-instance.offering-instance.list` | An event is generated when you list all software instances in an account. |
| `globalcatalog-instance.offering-instance.read` | An event is generated when you retrieve a software instance. |
| `globalcatalog-instance.offering-instance.retrieve_history` | An event is generated when you access the audit logs for a software instance. |
| `globalcatalog-instance.offering-instance.update` | An event is generated when you install updates to a software instance. |
| `globalcatalog-instance.dashboard.view` | An event is generated when you access the software instance details page. |
{: caption="Table 13. Actions that generate events for software instances" caption-side="top"}

## Events for managing tags
{: #at_events_acc_mgt_resources}

The following table lists the actions that generate an event:

| Action                                          | Description |
|-------------------------------------------------|-------------|
| `global-search-tagging.tag.create`              | An event is generated when you create a tag. The tag type is included in the requestData object. |
| `global-search-tagging.tag.delete`              | An event is generated when you delete a tag in your account.  |
| `global-search-tagging.tags.delete`             | An event is generated when you delete all the tags that are not attached to resources in your account.  |
| `<service-name>.tag.attach`                     | An event is generated when you associate a tag to a resource. |
| `<service-name>.tag.detach`                     | An event is generated when you remove a tag from a resource.  |
{: caption="Table 14. Actions that generate events" caption-side="top"}

When an access tag is created, you get an event with `global-search-tagging.tag.create`.

When an access tag is attached to a resource you get the event `<service-name>.tag.attach`.


## Events for managing users
{: #at_events_acc_mgt_users}

The following table lists the actions that generate an event:

| Action                               | Description |
|--------------------------------------|-------------|
| `user-management.user.invite`        | An event is generated when you invite a user to the account. |
| `user-management.user.resend-invite` | An event is generated when you resend a invite to a user for the account. |
| `user-management.cloud-user.list`    | An event is generated when you retrieve users from the account. |
| `user-management.user.read`          | An event is generated when you retrieve a user's information from the account. |
| `billing.user.active`                | An event is generated when a user, that has received an email invitation to join an account, verifies the email address. |
| `user-management.user.update`        | An event is generated when log in configurations are modified for a user from the {{site.data.keyword.cloud_notm}} UI. |
| `user-management.user-realm.update`  | An event is generated when you update a user's IBM ID. |
| `user-management.user.delete`        | An event is generated when you remove a user from the account. |
| `user-management.user-setting.read`  | An event is generated when you retrieve the user's login configuration settings: User one-time passcode authentication ,Require MFA security questions at login, User-managed login or Setting up security questions |
| `user-management.user-setting.update` | An event is generated when you update the user's login configuration settings: User one-time passcode authentication ,Require MFA security questions at login, User-managed login or Setting up security questions |
{: caption="Table 15. Actions that generate events" caption-side="top"}

### Inviting a user to an account
Separate events are generated for this asynchronous activity: one showing a pending invitation and one showing the completion or failure of the invitation.
* A pending invitation event would contain the following values for the action, outcome and message fields.
```json
"action": "user-management.user.invite",
"outcome": "pending",
"message": "IAM User Management: invite user -pending"
``` 
* A completed invitation event would contain the following values for the action, outcome and message fields
```json
"action": "user-management.user.invite",
"outcome": "success",
"message": "IAM User Management: invite user"
``` 

### Deleting a user from an account
Separate events are generated for asynchronous delete users requests: one showing a pending deletion and one showing the completion or failure of the delete
* A pending delete user event would contain the following values for the action, outcome and message fields
```json
"action": "user-management.user.delete",
"outcome": "pending",
"message": " IAM User Management: delete user IBMid-Example -pending"
``` 
* A completed delete user event would contain the following values for the action, outcome and message fields
```json
"action": "user-management.user.delete",
"outcome": "success",
"message": " IAM User Management: delete user IBMid-Example"
``` 
## Events for carbon calculator
{: #at_events_carbon_calculator}

The following table lists the actions that generate an event:

| Action                               | Description |
|--------------------------------------|-------------|
| `carbon-calculator.carbon-emissions.list`        | Request to get the carbon emissions for a given account. |
| `carbon-calculator.services.list`        | Request the list the services for which carbon emissions can be fetch. |
| `carbon-calculator.locations.list`        | Request the list of location from where carbon emissions can be fetch. |
{: caption="Table 16. Actions that generate events" caption-side="top"}

## Where to look for the events
{: #at_events_acc_mgt_ui}

Events are available in the **Frankfurt (eu-de)** region.

To view these events, you must [provision an instance](/docs/activity-tracker?topic=activity-tracker-provision#provision) of the {{site.data.keyword.at_full_notm}} service in the **Frankfurt (eu-de)** region. Then, you must [open the {{site.data.keyword.at_full_notm}} UI](/docs/activity-tracker?topic=activity-tracker-launch).


## Analyzing events
{: #at_events_analyze}




### Catalog events
{: #at_events_analyze_2}

You can find the value `unavailable` in catalog events. This value indicates when an update is made, but specific details about the update aren't included.
{: important}



### User management events
{: #at_events_analyze_3}

This section explains events that are generated when you manage users from the **Manage** &gt; **Access IAM** &gt; **Users** dashboard.

When you analyze user management events, `target.name` is set to the user ID of the user on which the action is requested.


#### Modify the status of a user
{: #at_events_analyze_3_1}

When you modify information about the user status from the **User Details** section, you get the following 2 events:
* Event with action `user-management.user.update` that reports a request in the account to modify the user's properties.
* Event with action `user-management.user-setting.update` that indicates the values of the user's properties after the update request completes.

Depending on the request, you might get additional events with action `user-management.user-setting.update`. If your account is a Lite one, you only get 1 event with action `user-management.user.update`.

For example, see the `requestData` field for the event `user-management.user-setting.update`:

```json
"action": "user-management.user-setting.update",
"message": "User management service: update user settings",
"requestData": {
    "2FA": false,
    "allowed_ip_addresses": "",
    "iam_id": "IBMid-xxxxxxx",
    "origin": "BSS",
    "security_questions_setup": false
}
```
{: screen}

#### Restrict IP addresses
{: #at_events_analyze_3_2}

When you configure IP address restrictions from the **IP address restrictions** section, you get 1 event with action `user-management.user-setting.update`.

For example, see the `requestData` field for the event `user-management.user-setting.update`:

```json
"action": "user-management.user-setting.update",
"message": "User management service: update user settings",
"requestData": {
    "allowed_ip_addresses": "14.15.98.123",
    "iam_id": "IBMid-xxxxxxx",
    "origin": "BSS"
}
```
{: screen}


#### Manage user's login
{: #at_events_analyze_3_3}

When you modify information about a user's login from the **Manage** &gt; **Access IAM** &gt; **Users** &gt; **User Details** section, you get 1 event with action `user-management.user-setting.update`.

See the sample of the `requestData` field when the **User-managed login:** property is disabled:

```json
"action": "user-management.user-setting.update",
 "message": "User management service: update user settings",
"requestData": {
    "iam_id": "IBMid-27000757DW",
    "origin": "BSS",
    "self_manage": false
}
```
{: screen}


See the sample of the `requestData` field when the **User one-time passcode authentication:** property is enabled. The `requestData.2FA` field is set to `true`.

```json
"action": "user-management.user-setting.update",
"message": "User management service: update user settings",
"requestData": {
    "2FA": true,
    "iam_id": "IBMid-xxxxx",
    "origin": "BSS",
    "security_questions_setup": true,
    "self_manage": false
 }
}
```
{: screen}

See the sample of the `requestData` field when the **Require MFA security questions at login:** property is enabled. The `requestData.security_questions_setup` field is set to `true`.

```json
"action": "user-management.user-setting.update",
"message": "User management service: update user settings",
"requestData": {
    "2FA": true,
    "iam_id": "IBMid-xxxxxx",
    "origin": "BSS",
    "security_questions_setup": true,
    "self_manage": false
 }
}
```
{: screen}




#### requestData fields
{: #at_events_analyze_3_reqdata}

The following table lists *requestData* fields that you can find in events that are generated when user details are modified from the **Users** dashboard:

| Field | Type | Description |
|-------|------|-------------|
| `2FA`                      | Boolean         | Defines the MFA requirements for users in the account.   \n This field is set to `true` when MFA is enabled for users.  |
| `allowed_ip_addresses`     | String          | List of IP addresses from where a user is allowed to access account resources. |
| `iam_id`                   | String          | Defines the IBM ID of the user whose settings are being modified. |
| `security_questions_setup` | Boolean         | Defines when a user requires security questions to log in to the account.   \n This field is set to `true` to indicate that questions are required.  |
| `self_manage`              | Boolean         | Defines whether a user can configure his log in settings on how to log in to the account.    \n This field is set to `true` to allow a user to set password expiration, turn on security questions for login, and define allowed IP addresses for log in to {{site.data.keyword.cloud_notm}} and from classic infrastructure API calls.  |
{: caption="Table 17. User management requestData fields" caption-side="top"}



### Events for managing account usage reports
{: #at_events_analyze_4}

This section explains events that are generated when a user looks at the information that is provided through the  **Manage** &gt; **Billing and usage** &gt; **Usage** section, or request an export of the data.

You can get events with `reason.reasonCode = 404` that are generated when there is no usage data available for the request. The `severity` is set to normal.
{: note}

#### requestData fields
{: #at_events_analyze_4_reqdata}

The following table lists the fields that are available through the `requestData` field in the events with actions `billing.account-summary.read`, `billing.account-summary.download`, and `billing.account-instances-usage-report.download`:

| Field | Type | Description | Status |
|-------|------|-------------|--------|
| `month` | String | Indicates the month that the user selects to view usage data. | Included always in the event |
{: caption="Table 18. Account usage summary requestData fields" caption-side="top"}


The following table lists the fields that are available through the `requestData` field in the events with actions `billing.account-usage-report.read`:

| Field               | Type      | Description | Status |
|---------------------|-----------|-------------|--------|
| `month`             | String    | Indicates the month that the user selects to view usage data. |  Included always in the event |
| `usage_report_type` | String    | Indicates the type of report.   \n Valid values are `instances` and `rollup`.|  Included always in the event |
| `sub_account_id`    | String    | Indicates the sub-account ID. | Optional |
| `resource_group`    | String    | Indicates the resource group. | Optional   \n Included if the user filters data by resource group. |
| `organization_id`   | String    | Indicates the organization ID. | Optional |
| `daily`             | Boolean   | Indicates the frequency of the report. | Optional |
{: caption="Table 19. Account usage requestData fields" caption-side="top"}


The following table lists the fields that are available through the `requestData` field in the events with actions `billing.enterprise-usage-report.read` and `billing.enterprise-usage-report.download`:

| Field               | Type      | Description | Status |
|---------------------|-----------|-------------|--------|
| `month`             | String    | Indicates the month that the user selects to view usage data. |  Included always in the event |
| `children`          | Boolean   | Indicates whether the usage is aggregated at account level. | Included always in the event |
| `enterprise_id`     | String    | Indicates the ID of the enterprise. |  Included always in the event |
| `account_id`        | String    | Indicates the sub-account ID that is requested in the report. | Optional |
| `account_group_id`  | String    | Indicates the account group when a user selects one. | Optional   \n Included if the user filters data by selecting 1 account group. |
{: caption="Table 20. Enterprise usage requestData fields" caption-side="top"}


The following table lists the fields that are available through the `requestData` field in the events with actions `billing.enterprise-instances-usage-report.download`:

| Field               | Type      | Description | Status |
|---------------------|-----------|-------------|--------|
| `month`             | String    | Indicates the month that the user selects to view usage data. |  Included always in the event |
| `enterprise_id`     | String    | Indicates the ID of the enterprise. |  Included always in the event |
| `account_id`        | String    | Indicates the the sub-account IDs that is requested in the report. | Optional |
| `account_group_id`  | String    | Indicates the account group when a user selects one. | Optional   \n Included if the user filters data by selecting 1 account group. |
{: caption="Table 21. Enterprise instances usage requestData fields" caption-side="top"}




### Account IAM settings events (Deprecated)
{: #at_events_analyze_1}

This section explains events that are generated when you configure the IAM account settings from the **Access (IAM)** &gt; **Settings** dashboard.

#### Configuring MFA
{: #at_events_analyze_1_1}

When you set on MFA in your account by configuring the **Account Login** section in the **Access (IAM)** &gt; **Settings** dashboard, you get 2 events:
* Event with action `billing.account-traits.update` that reports the type of MFA that is configured in the account in the `requestData.mfa` field.
* Event with action `billing.account-mfa.set-on` that indicates that MFA is enabled in the account.

When you set off MFA, you get the following 2 events:
* Event with action `billing.account-traits.update` that reports the type of MFA that is configured in the account in the `requestData.mfa` field.
* Event with action `billing.account-mfa.set-off` that indicates that MFA is disabled in the account.

For example, see the `requestData` field for the event `billing.account-traits.update`:

```json
"action": "billing.account-traits.update",
"message": "Billing service: update account traits",
"requestData": {
    "mfa": "",
    "origin": "BSS"
}
```
{: screen}

#### Configuring user list visibility restriction
{: #at_events_analyze_1_2}

When you modify the *User list visibility restriction* IAM account setting in the **Manage** &gt; **Access (IAM)** &gt; **Settings** dashboard, you get 1 event with action `billing.account-traits.update`.

For example, see the `requestData` field for the event `billing.account-traits.update`:

```json
"action": "billing.account-traits.update",
"message": "Billing service: update account traits",
"requestData": {
    "origin": "BSS",
    "team_directory_enabled": false
}
```
{: screen}

#### requestData fields
{: #at_events_analyze_1_reqdata}

The following table lists *requestData* fields that you can find in events that are generated when the IAM account settings are modified from the **Access (IAM)** &gt; **Settings** dashboard:


| Field | Type | Description |
|-------|------|-------------|
| `team_directory_enabled`   | Boolean         | Defines the status of the *User list visibility restriction* IAM account setting.   \n When it is set to `true`, users in your account can view other users from the Users page. |
| `mfa`                      | String          | Defines the MFA method that is required for users to log in to the account.   \n Valid values are *TOTP*, and *TOTP4ALL*   \n This field is set to `TOTP` when the account requires MFA for non-federated users only. Users are required an ID, password, and a time-based one-time passcode to log in.   \n This field is set to `TOTP4ALL` when the account requires MFA for all users.  \n All users by requiring an ID, password, and a time-based one-time passcode.   \n When this field is empty, MFA is not enabled in the account, and all users log in by using a standard ID and password. |
{: caption="Table 22. Account IAM settings requestData fields" caption-side="top"}
