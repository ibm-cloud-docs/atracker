---

copyright:
  years: 2019, 2024
lastupdated: "2024-03-01"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}


# Required actions for newly supported regions
{: #new_region_support}

{{site.data.keyword.atracker_full}} is planned to be supported in the br-sao, ca-tor, jp-osa, jp-tok and in-che regions in April 2024. As a result, all existing customers need to evaluate their {{site.data.keyword.atracker_full_notm}} configurations and make any required changes.
{: shortdesc}

## Check whether you have the right permissions
{: #new_region_1}

Log in to the {{site.data.keyword.cloud_notm}} by using an ID with {{site.data.keyword.iamshort}} with [Administrator permissions.](/docs/atracker?topic=atracker-iam)

## Check whether the routing rules capture events for the new regions
{: #new_region_2}

With routing rules, you can change the destination (the target) where AT events flow based on the region of the AT events. This routing includes global events.

The routing rules determine which events are matched for routing.

Run the command `ibmcloud at route ls`.

This example shows a route where events from all locations (all regions and global events) are routed to a target.

```text
$ ibmcloud at route ls
OK
Name                         ID                                     Rules                                                      Route Version   API version   CreatedAt                  UpdatedAt
es_demo_route                021ab990-6799-4a99-bb9b-99b4fe26abfc   [[aa345799-99c2-9982-99a8-1e9954926295],[*]]               0               2             2023-11-28T17:00:30.701Z   2023-11-28T17:00:30.701Z
```
{: screen}

If you have a configuration similar to this example, where there is a wildcard (`*`) location that is defined in the routing rule, then all of your events will be routed to that target when the new {{site.data.keyword.atracker_full_notm}} regions are enabled.

This example shows a route where only the global events are routed to a target. All of the regional events are not processed and are discarded.

```text
$ ibmcloud at route ls
OK
Name                         ID                                     Rules                                                      Route Version   API version   CreatedAt                  UpdatedAt
global-to-cos                08199417-9ec7-4d99-b9b4-41cd2b1b99a1   [[cded994e-a999-9cc9-b499-24099955d286],[global]]          0               2             2023-05-26T12:52:53.536Z   2023-05-26T12:52:53.536Z
```
{: screen}

If you have a configuration similar to this example, and only a subset of regions (or global) are listed, then you need to either add the newly supported regions to your configuration, or change the location to use the wildcard (`*`) location.

For more information about configuring routes, see [Managing routes.](/docs/atracker?topic=atracker-route_v2&interface=cli)
{: tip}

## Check whether a default target is configured in your account
{: #new_region_3}

If you do not have a route that is configured, check if you have a default target that is configured in your account.

The default target in the {{site.data.keyword.atracker_full_notm}} settings is the destination where activity tracker (AT) events are sent if there are no routing rules that match an event’s region.

Run the command `ibmcloud at setting get`.

The “Default targets” array shows up to 2 defined targets that receive AT events, if there is no match in the routing definition.

For example, this shows that there are no default targets configured.

```text
$ ibmcloud at setting get
OK
IBM Cloud Activity Tracker Event Routing settings
Metadata region primary:                             us-south
Metadata region backup:                              us-east
Default targets:                                     [ ]
```
{: screen}

This example shows that a default target is configured.

```text
$ ibmcloud at setting get
OK
IBM Cloud Activity Tracker Event Routing settings
Metadata region primary:                             us-south
Metadata region backup:                              us-east
Default targets:                                     [“aa345994-79c2-4592-99a8-1e1994926295”]
```
{: screen}

For more information about defining targets, see [Managing targets](/docs/atracker?topic=atracker-target_v2&interface=cli).
{: tip}

If you have a default target defined, then events not matching your account’s routing rules will be routed to the default targets and you are not affected by this change.

If you do not have a default target defined, then continue to the next step.

## Define a default target
{: #new_region_4}

Unless you are specifically trying to drop AT events, using the default target is the best way to ensure that all data is retained somewhere.  You can configure a default target with a command similar to `ibmcloud at setting update --default-target <target-id>`.

For example:

```text
$ ibmcloud at setting update --default-targets aa34579944-99c2-4592-99a8-1e1994926295
Are you sure you want to update the IBM Cloud Activity Tracker Event Routing settings for your account? [y/N]> y
OK
IBM Cloud Activity Tracker Event Routing settings
Metadata region primary:                             us-south
Metadata region backup:                              us-east
Default targets:                                     [aa34579944-99c2-4592-99a8-1e1994926295]
```
{: screen}




