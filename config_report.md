---

copyright:
  years: 2019, 2023
lastupdated: "2022-05-05"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Generating a report of {{site.data.keyword.atracker_short}} resources
{: #config_report}

You can validate your account configuration for {{site.data.keyword.atracker_full}} by generating a report of the {{site.data.keyword.atracker_full_notm}} resources using the {{site.data.keyword.atracker_full_notm}} CLI.
{: shortdesc}

The V1 API is deprecated. This CLI and API can only be used while using the {{site.data.keyword.atracker_full_notm}} V1 API.  Once you have [migrated to the V2 API](/docs/atracker?topic=atracker-migrate-resources) this CLI and API can no longer be used.
{: deprecated}

## Prereqs
{: #route-report-prereqs}

Before you use the CLI to generate your {{site.data.keyword.atracker_full_notm}} resources report, complete the following steps:

1. Identify the endpoint in the region where you need the report. For more information, see [Endpoints](/docs/atracker?topic=atracker-endpoints#endpoints_api).

    Change the link to be direct to the Atracker endpoints (Event Routing ones)
    {: note}

2. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

3. [Install the {{site.data.keyword.atracker_full_notm}} CLI](/docs/atracker?topic=atracker-activity-tracking-cli#activity-tracking-cli-prereq).


## Running the report
{: #route-report-running}

Use the following command to return a report about the {{site.data.keyword.atracker_full_notm}} service configuration.  This report will include any issues in the configuration.

```text
ibmcloud atracker config report --output YAML
```
{: pre}

Output similar to the following will be returned:

```text
OK
summary: The IBM Cloud Activity Tracker service configuration has detected some warnings. Review the warnings section for details. All global IBM Cloud Activity Tracker service events are being forwarded to a target [au-syd-default-cse-target-0] in the region [au-syd].
warnings:
- The target [us-south-default-target] of the route [us-south-default-cse-route] defined in the region [us-south] has a write issue. An error is reported as api key is not valid since 2021-06-20T01:48:28.497Z.
- No route is defined for the us-east region. All IBM Cloud Activity Tracker service events are forwarded to LogDNA for that region.
config-report:
- region: au-syd
  route:
    route-name: au-syd-default-cse-route
    global-events: true
    target:
      target-name: au-syd-default-cse-target-0
      target-type: cloud_object_storage
      cos-target:
        bucket: prod-au-syd
        write-status: success
- region: us-south
  route:
    route-name: us-south-default-cse-route
    global-events: false
    target:
      target-name: us-south-default-target
      target-type: cloud_object_storage
      cos-target:
        bucket: prod-us-south
        write-status: '-'
- region: us-east
```
{: screen}

If no configuration is available for the region, the region will be listed with no data under it.
{: note}
