---

copyright:
  years: 2019, 2022
lastupdated: "2022-08-08"

keywords: 

subcollection: atracker

---

{{site.data.keyword.attribute-definition-list}}

 
# IAM actions by role
{: #iam_by_role}

The following tables show the {{site.data.keyword.atracker_short}} actions by role.
{: shortdesc}

For {{site.data.keyword.atracker_short}}, the IAM actions and Activity Tracker actions are the same.
{: note}

 
## Operator
{: #iam_by_role_operator}


| Platform role | Activity Tracker action | Action |
|---------------|-------------------------|-------------|
| Operator      | `atracker.target.read`  | View a target |
| Operator      | `atracker.route.read`   | View a route |
| Operator      | `atracker.endpoint.get` | View endpoint properties `[V1]` |
| Operator      | `atracker.setting.get`  | View configuration settings `[V2]` |
| Operator      | `atracker.migration.get` | View migration status `[V2]` |
| Operator      | `atracker.target.list`  | List all targets |
| Operator      | `atracker.route.list`   | List all routes |
{: caption="Table 1. {{site.data.keyword.atracker_short}} actions for the operator role" caption-side="top"}

## Viewer
{: #iam_by_role_viewer}

| Platform role | Activity Tracker action | Action |
|---------------|-------------------------|-------------|
| Viewer | `atracker.target.read` | View a target |
| Viewer | `atracker.route.read` | View a route |
| Viewer | `atracker.endpoint.get` | View endpoint properties `[V1]` |
| Viewer | `atracker.setting.get` | View configuration settings `[V2]` |
| Viewer | `atracker.migration.get` | View migration status `[V2]` |
| Viewer | `atracker.target.list` | List all targets |
| Viewer | `atracker.route.list` | List all routes |
{: caption="Table 2. {{site.data.keyword.atracker_short}} actions for the viewer role" caption-side="top"}

## Editor
{: #iam_by_role_editor}


| Platform role | Activity Tracker action | Action |
|---------------|-------------------------|-------------|
| Editor | `atracker.target.read` | View a target |
| Editor | `atracker.route.read` | View a route |
| Editor | `atracker.endpoint.get` | View endpoint properties `[V1]` |
| Editor | `atracker.setting.get` | View configuration settings `[V2]` |
| Editor | `atracker.migration.get` | View migration status `[V2]` |
| Editor | `atracker.target.create` | Create a target |
| Editor | `atracker.route.create` | Create a route |
| Editor | `atracker.target.update` | Update a target |
| Editor | `atracker.route.update` | Update a route |
| Editor | `atracker.target.delete` | Delete a target |
| Editor | `atracker.route.delete` | Delete a route |
| Editor | `atracker.target.list` | List all targets |
| Editor | `atracker.route.list` | List all routes |
{: caption="Table 3. {{site.data.keyword.atracker_short}} actions for the editor role" caption-side="top"}


## Administrator
{: #iam_by_role_admin}

| Platform role | Activity Tracker action | Action |
|---------------|-------------------------|-------------|
| Administrator | `atracker.target.read` | View a target |
| Administrator | `atracker.route.read` | View a route |
| Administrator | `atracker.endpoint.get` | View endpoint properties `[V1]` |
| Administrator | `atracker.setting.get` | View configuration settings `[V2]` |
| Administrator | `atracker.endpoint.set` | Set endpoint properties `[V1]` |
| Administrator | `atracker.target.create` | Create a target |
| Administrator | `atracker.route.create` | Create a route |
| Administrator | `atracker.target.update` | Update a target |
| Administrator | `atracker.route.update` | Update a route |
| Administrator | `atracker.target.delete` | Delete a target |
| Administrator | `atracker.route.delete` | Delete a route |
| Administrator | `atracker.target.list` | List all targets |
| Administrator | `atracker.route.list` | List all routes |
| Administrator | `atracker.setting.update` | Update configuration settings `[V2]` |
| Administrator | `atracker.migration.post` | Start migration `[V2]` |
| Administrator | `atracker.migration.get` | View migration status `[V2]` |
{: caption="Table 4. {{site.data.keyword.atracker_short}} actions for the administrator role" caption-side="top"}

`[V2]` is only applicable once you have [migrated to the V2 configuration.](/docs/activity-tracker?topic=activity-tracker-migration)  `[V1]` is only applicable to the V1 configuration and is unavailable after you migrate to the V2 configuration. All others are applicable to both configurations.
{: note}



