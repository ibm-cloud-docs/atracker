---

copyright:
  years: 2019, 2023
lastupdated: "2023-07-17"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Determining your {{site.data.keyword.atracker_full_notm}} configuration version
{: #get-config-version}

To collect auditing events in your {{site.data.keyword.cloud_notm}} account, you can configure {{site.data.keyword.atracker_short}} by using the {{site.data.keyword.atracker_short}} API or the {{site.data.keyword.atracker_short}} CLI.
{: shortdesc}

The V1 configuration is no longer supported.
{: deprecated}

## IAM permissions
{: #get-config-version-iam}

You must grant users IAM permissions to manage the account settings. For more information, see [Assign access to resources](/docs/account?topic=account-assign-access-resources).

When you define a policy, you can must set the scope of the policy to the account. A route is a global resource that is not bound to a specific region.
{: note}

| IAM action               | IAM Policy scope  | IAM Roles                          | Description         |
| ------------------------ | ----------------- | ---------------------------------- | -------------- |
| `atracker.setting.get`    | Account        | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | Get setting information |
| `atracker.setting.update` | Account        | `Administrator`| Update settings |
{: caption="Table 1. Required IAM roles to manage the {{site.data.keyword.atracker_short}} account settings." caption-side="top"}



## Determining your CLI version
{: #get-config-version-cli-version}

To configure {{site.data.keyword.atracker_short}} you must have the current (V2) API and CLI installed.

If you are unsure if your CLI environment is running the current configuration, run the following command:

```text
ibmcloud atracker setting get
```
{: pre}

If the command indicates that `setting` is not a valid command, then you do not have the current CLI installed.

Install the current CLI by running the following command:

```text
ibmcloud plugin install atracker
```
{: pre}

Update the current CLI by running the following command:

```text
ibmcloud plugin update atracker
```
{: pre}
