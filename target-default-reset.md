---

copyright:
  years: 2019, 2022
lastupdated: "2022-08-12"

keywords: 

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Reseting the default targets in the account
{: #target-default-reset}

To reset the {{site.data.keyword.atracker_short}} account's default targets, you must delete any default targets from the account configuration. 
{: shortdesc}


## Prereqs
{: #target-default-reset-prereqs}

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-atracker-cli-config).

3. Check that you have IAM permissions to read and update the {{site.data.keyword.atracker_short}} account settings. 

| Role                      | Minimum scope  | Minimum required roles | Action         |
| ------------------------- | -------------- | ---------------------- | -------------- |
| `atracker.setting.get`    | Account        | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | Get setting information |
| `atracker.setting.update` | Account        | `Administrator`| Update settings |
{: caption="Table 1. Required IAM roles to manage the {{site.data.keyword.atracker_short}} account settings." caption-side="top"}

Next, log in to {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)



## Step 1. Identify targets
{: #target-default-reset-step1}

Get the list of targets that are defined in the account. Run the following command:

```
ibmcloud atracker target ls
```
{: pre}


## Step 2. Check your current account settings
{: #target-default-reset-step2}

To check your account's configuration and find out if there are default targets configured, run the following command:

```
ibmcloud atracker setting get
```
{: pre}

The setting **Default targets** lists any targets in the account that have been configured as default targets.

## Step 3. Reset the default targets
{: #target-default-reset-step3}

Run the following command to reset the account's defaul targets:

```sh
ibmcloud atracker setting update  --default-targets ""
```
{: pre}






