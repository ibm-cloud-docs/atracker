---

copyright:
  years:  2021, 2025
lastupdated: "2025-04-15"

keywords:

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

# Changes to {{site.data.keyword.cos_full_notm}} file naming convention
{: #change_cos_filename_convention}

For {{site.data.keyword.cos_full}} targets (target type = `cos`), the auditing events are routed to the corresponding {{site.data.keyword.cos_full_notm}} (COS) buckets and stored in time-based files. The file naming convention is being changed. The format of the data in the files is not changed.

The following is the current naming convention, where `<region>` is the COS target's region and `<timestamp>` is in UTC.

```text
<region>/<date and hour>/<timestamp>+<offset>.log
```
{: codeblock}

An example of the current COS file name: `us-south/2025-04-10T00/2025-04-10T00:01+00.log`

The new naming convention has 2 updates:

- Prepend the source account ID for the events to the path to allow consolidation of events from multiple accounts in the same COS bucket.
- Append a unique ID to the file name to permit multiple writers and avoid file name collisions.

```text
<account_id>/<region>/<date and hour>/<timestamp>+<offset>_<uuid>.log
```
{: codeblock}

An example of the new COS file name: `f12375ed17a24ecfb1f32afcf47285f3/us-south/2025-04-10T21/2025-04-10T21:02+01_0196361c-7836-7cdd-808c-92a417338cbd.log`

Before 15 May 2025, customers that have a dependency on the current file naming convention might need to update their automation to reference the common file name prefix to handle both the current and new conventions.

- If your automation tool does not use a prefix to list objects in a COS bucket, no action is required.

- If your automation tool uses a prefix to list objects (for example, files) in a COS bucket, update the automation so that it can list objects with both the old and new naming conventions.
    - A simple approach is to list objects twice, first in the old naming convention and then in the new naming convention, so that you can get the objects regardless of the old or new naming convention.
    - The list call for the old naming convention can be removed after 15 May 2025.
