---

copyright:
  years: 2019, 2023
lastupdated: "2021-08-09"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Managing service instances (WIP)
{: #service_instance_events}


{{site.data.keyword.at_full_notm}} events
{: shortdesc}

This information applies only to {{site.data.keyword.at_full}} event viewing.
{: important}


| Working with services                   | Service     | Actions                                        |
|:----------------------------------------|:------------|:-----------------------------------------------|
| `Provision an instance`                 | `BSS`       | `<serviceName>.instance.create` |
| `Delete an instance`                    | `BSS`       | `<serviceName>.instance.delete`   \n `iam-am.policy.delete` (3 events of these type) |
| `Delete an instance with a tag`         | `BSS`       | `<serviceName>.instance.delete` |
| `Rename an instance`                    | `BSS`       | `<serviceName>.instance.update` |
| `Add a tag to an instance`              | `BSS`       | `global-search-tagging.tag.attach-tag` |
{: caption="Table 1. Service actions" caption-side="bottom"}





```text
6/Dec/2019:10:14:04 BSS IBM Cloud Activity Tracker with LogDNA: create instance at-logdna-tokyo
```


```text
6/Dec/2019:09:38:32 BSS IBM Log Analysis with LogDNA: create instance logdna-via-cli
6/Dec/2019:09:42:03 BSS IBM Log Analysis with LogDNA: create instance logdna-via-ui
6/Dec/2019:09:42:04 iam-am IAM Access Management: create policy
6/Dec/2019:09:42:04 iam-identity IAM Identity Service: create account-serviceid logdna-via-ui-key-admin
6/Dec/2019:09:42:04 iam-identity IAM Identity Service: create serviceid-apikey logdna-via-ui-key-admin
6/Dec/2019:09:42:05 BSS logdna: create key logdna-via-ui-key-admin
6/Dec/2019:09:42:05 iam-am IAM Access Management: create policy
```


```text
6/Dec/2019:10:13:35 BSS IBM Cloud Activity Tracker with LogDNA: delete instance at-logdna-tokyo
6/Dec/2019:10:13:36 iam-am IAM Access Management: delete policy
6/Dec/2019:10:13:36 iam-am IAM Access Management: delete policy
6/Dec/2019:10:13:36 iam-am IAM Access Management: delete policy
```

```text
6/Dec/2019:10:26:39 iam-am IAM Access Management: create policy
6/Dec/2019:10:26:39 iam-identity IAM Identity Service: create account-serviceid logdna-via-cli-key-admin
6/Dec/2019:10:26:39 iam-identity IAM Identity Service: create serviceid-apikey logdna-via-cli-key-admin
6/Dec/2019:10:26:39 iam-am IAM Access Management: create policy
```





| Action                                          | Description |
|-------------------------------------------------|-------------|
| `global-search-tagging.tag.attach`              | An event is generated when you associate a tag to a resource. |
| `global-search-tagging.tag.detach`              | An event is generated when you remove a tag from a resource.  |
| `global-search-tagging.tag.update`              | An event is generated when you update a tag that is attached to a resource.  |
| `global-search-tagging.tag.delete`              | An event is generated when you delete a tag in your account.  |
| `global-search-tagging.tag.deleteall`           | An event is generated when you delete all the tags that are not attached to resources in your account.  |
{: caption="Table 4. Actions that generate events" caption-side="top"}
