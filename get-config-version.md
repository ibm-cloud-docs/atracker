---

copyright:
  years: 2019, 2022
lastupdated: "2022-05-16"

keywords: 

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Determining your {{site.data.keyword.atracker_full_notm}} configuration version
{: #get-config-version}

To collect auditing events in your {{site.data.keyword.cloud_notm}} account, you can configure {{site.data.keyword.atracker_short}} by using the {{site.data.keyword.atracker_short}} API or the {{site.data.keyword.atracker_short}} CLI. You can have a V1 configuration or a V2 configuration.
{: shortdesc}



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

To use the V2 configuration you must have the V2 API and CLI installed.

If you are unsure if your CLI environment is running the V2 configuration, run the following command:

```text
ibmcloud atracker setting get
```
{: pre}

If the command indicates that `setting` is not a valid command, then you do not have the V2 CLI installed. 

Install the V2 CLI by running the following command:

```text
ibmcloud plugin install atracker
```
{: pre}

Update the V2 CLI by running the following command:

```text
ibmcloud plugin update atracker
```
{: pre}

## Determining if you have V1 routes and targets
{: #get-config-version-conf-version}

Once you have upgraded to the V2 CLI you can run the following command to check the configuration version running in your {{site.data.keyword.atracker_full}} deployment.

```text
ibmcloud atracker setting get
```
{: pre}

If the response shows your deployment is running V1, you will need to [migrate your route and target configuration to a V2 configuration.](/docs/atracker?topic=atracker-migrate-resources)


## Next steps
{: #get-config-version-v2-next-steps}

If [step 1](#cli_version) and [step 2](#conf_version) show you have a V2 configuration, or you have completed the migration in step 2, if needed, you are ready to create and manage your {{site.data.keyword.atracker_full}} instance using the V2 configuration.

If you have a V1 configuration, migrate to a V2 configuration. For more information, see [Migrating the {{site.data.keyword.atracker_short}} account configuration from V1 to V2](/docs/atracker?topic=atracker-migration&interface=cli). 


