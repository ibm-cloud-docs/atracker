---

copyright:
  years: 2019, 2023
lastupdated: "2022-05-25"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Creating a report of the {{site.data.keyword.atracker_short}} V2 configuration
{: #config_report_v2}

After configuring your {{site.data.keyword.atracker_full}} resources for your account, you should save a copy of your configuration for reference and backup purposes.
{: shortdesc}

## Prereqs
{: #config_report_v2_prereqs}

Before you use the CLI to save your {{site.data.keyword.atracker_full_notm}} resource data, you must do the following:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-activity-tracking-cli#activity-tracking-cli-prereq).

3. Make sure your account is [running the V2 configuration.](/docs/atracker?topic=atracker-settings&interface=cli#settings-get-cli)  If you are running the V1 configuration [migrated to the {{site.data.keyword.atracker_full_notm}} V2 configuration](/docs/atracker?topic=atracker-migration).

4. Make sure you have configured your [settings](/docs/atracker?topic=atracker-settings), [routes](/docs/atracker?topic=atracker-route_v2), and [targets](/docs/atracker?topic=atracker-atracker-resources&interface=cli#atracker-resources-targets).


## Saving a copy of your account settings
{: #save_settings}

Run the following command to save a copy of your account settings to a file.

```text
ibmcloud atracker setting get --output JSON > ACCOUNT_settings.json
```
{: pre}

Where `ACCOUNT` is a unique indicator for your account.

## Saving a copy of your route configuration
{: #save_route}

Run the following command to save a copy of your route configuration to a file.

```text
ibmcloud atracker route ls --output JSON > ACCOUNT_routes.json
```
{: pre}

Where `ACCOUNT` is a unique indicator for your account.

## Saving a copy of your target configuration
{: #save_target}

Run the following command to save a copy of your target configuration to a file.

```text
ibmcloud atracker target ls --output JSON > ACCOUNT_targets.json
```
{: pre}

Where `ACCOUNT` is a unique indicator for your account.
