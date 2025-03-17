---

copyright:
  years:  2021, 2025
lastupdated: "2025-03-17"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Changes to {{site.data.keyword.cos_full_notm}} file naming convention
{: #change_cos_filename_convention}

For {{site.data.keyword.cos_full}} targets (target type = `cos`), the auditing events are routed to the corresponding {{site.data.keyword.cos_full_notm}} (COS) buckets and stored in time-based files. The file naming convention is being changed. The format of the data in the files is not changed.

The current naming convention is:

```text
<region>/<date and hour>/<timestamp>+<offset>.log
```
{: codeblock}

With the change, the new naming convention appends a unique ID to the current naming convention:

```text
<region>/date and hour>/<timestamp>+<offset>_<uuid>.log
```
{: codeblock}

Customers that have a dependency on the current file naming convention might need to update automation referencing the file naming to the new naming convention. 
