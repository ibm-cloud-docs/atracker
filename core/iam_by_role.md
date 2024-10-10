---

copyright:
  years:  2021, 2024
lastupdated: "2024-10-09"

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
| Operator      | `atracker.setting.get`  | View configuration settings  |
| Operator      | `atracker.target.list`  | List all targets |
| Operator      | `atracker.route.list`   | List all routes |
{: caption="{{site.data.keyword.atracker_short}} actions for the operator role" caption-side="top"}

## Viewer
{: #iam_by_role_viewer}

| Platform role | Activity Tracker action | Action |
|---------------|-------------------------|-------------|
| Viewer | `atracker.target.read` | View a target |
| Viewer | `atracker.route.read` | View a route |
| Viewer | `atracker.setting.get` | View configuration settings |
| Viewer | `atracker.target.list` | List all targets |
| Viewer | `atracker.route.list` | List all routes |
{: caption="{{site.data.keyword.atracker_short}} actions for the viewer role" caption-side="top"}

## Editor
{: #iam_by_role_editor}

| Platform role | Activity Tracker action | Action |
|---------------|-------------------------|-------------|
| Editor | `atracker.target.read` | View a target |
| Editor | `atracker.route.read` | View a route |
| Editor | `atracker.setting.get` | View configuration settings  |
| Editor | `atracker.target.create` | Create a target |
| Editor | `atracker.route.create` | Create a route |
| Editor | `atracker.target.update` | Update a target |
| Editor | `atracker.route.update` | Update a route |
| Editor | `atracker.target.delete` | Delete a target |
| Editor | `atracker.route.delete` | Delete a route |
| Editor | `atracker.target.list` | List all targets |
| Editor | `atracker.route.list` | List all routes |
{: caption="{{site.data.keyword.atracker_short}} actions for the editor role" caption-side="top"}


## Administrator
{: #iam_by_role_admin}

| Platform role | Activity Tracker action | Action |
|---------------|-------------------------|-------------|
| Administrator | `atracker.target.read` | View a target |
| Administrator | `atracker.route.read` | View a route |
| Administrator | `atracker.setting.get` | View configuration settings |
| Administrator | `atracker.target.create` | Create a target |
| Administrator | `atracker.route.create` | Create a route |
| Administrator | `atracker.target.update` | Update a target |
| Administrator | `atracker.route.update` | Update a route |
| Administrator | `atracker.target.delete` | Delete a target |
| Administrator | `atracker.route.delete` | Delete a route |
| Administrator | `atracker.target.list` | List all targets |
| Administrator | `atracker.route.list` | List all routes |
{: caption="{{site.data.keyword.atracker_short}} actions for the administrator role" caption-side="top"}
