---

copyright:
  years: 2019, 2023
lastupdated: "2022-08-12"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Enforcing target locations
{: #target-locations}

To enforce target locations in your {{site.data.keyword.cloud_notm}} account, you must configure {{site.data.keyword.atracker_short}} account settings to limit the locations.
{: shortdesc}


## Prereqs
{: #target-locations-prereqs}

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-atracker-cli-config).

3. Check that you have IAM permissions to read and update the {{site.data.keyword.atracker_short}} account settings.

| Role                      | Minimum scope  | Minimum required roles | Action         |
| ------------------------- | -------------- | ---------------------- | -------------- |
| `atracker.setting.get`    | Account        | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` | Get setting information |
| `atracker.setting.update` | Account        | `Administrator`| Update settings |
{: caption="Table 1. Required IAM roles to manage the {{site.data.keyword.atracker_short}} account settings." caption-side="top"}


Next, log in to {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)



## Step 1. Get details of your current account settings
{: #target-default-step1}

Get details of your current account settings. Run the following command:

```text
ibmcloud atracker setting get
```
{: pre}

The setting **Permitted target regions** list all the locations where you allowd administrators to configure targets in the account.

## Step 2.
{: #target-default-step2}

To manage the list of permitted regions, run the following command:

```text
ibmcloud atracker setting update --permitted-target-regions REGIONS
```
{: pre}

Where `REGIONS` define a comma-separated list of regions.

For example, you can run the following command to set 3 regions only:

```text
ibmcloud atracker setting update --permitted-target-regions "us-south","us-east","eu-de"
```
{: screen}
