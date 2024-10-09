---

copyright:
  years:  2021, 2024
lastupdated: "2024-10-09"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Enforcing default targets
{: #target-default}

You can configure 1 or more default targets for events that are not explicitly managed in the {{site.data.keyword.atracker_short}} account's routing rules.
{: shortdesc}


## Prereqs
{: #target-default-prereqs}

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-atracker-cli-config).

3. Check that you have IAM permissions to read and update the {{site.data.keyword.atracker_short}} account settings.

| Role                      | Minimum scope  | Minimum required roles | Action         |
| ------------------------- | -------------- | ---------------------- | -------------- |
| `atracker.setting.get`    | Account        | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | Get setting information |
| `atracker.setting.update` | Account        | `Administrator`| Update settings |
{: caption="Required IAM roles to manage the {{site.data.keyword.atracker_short}} account settings." caption-side="top"}

Next, log in to {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)



## Step 1. Identify targets
{: #target-default-step1}

Get the list of targets that are defined in the account. Run the following command:

```text
ibmcloud atracker target ls
```
{: pre}

Copy the **ID** value of the targets that you want to configure in the account.

## Step 2. Check your current account settings
{: #target-default-step2}

To check your account's configuration and find out if there are default targets configured, run the following command:

```text
ibmcloud atracker setting get
```
{: pre}

The setting **Default targets** lists any targets in the account that have been configured as default targets.

## Step 3. Configure default targets
{: #target-default-step3}

Check the list of IDs for the targets that you want to configure and identify the ones that are not configured. Then, run the following command to configure the default targets in the account:

When you run the command, make sure that you include the target IDs of all the default targets in the account. The command replaces the exiting configuration with the new one.
{: important}

```sh
ibmcloud atracker setting update  --default-targets TARGETS
```
{: pre}

Where `TARGETS` represent the list of comma-separated target IDs.
