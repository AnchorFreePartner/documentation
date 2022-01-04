---
description: >-
  Learn how to get project data in CSV format for further processing or
  reporting
---

# Export Data

You can export 3 types of data:

* Project users (all users)&#x20;
* User's devices (all devices)&#x20;
* User's sessions (period of 1-30 days)

## Export history

The history of project data export is represented on the "Export data" page:

![Export data page](../.gitbook/assets/export\_list.png)

| Name     | Description                                                                                                                                                                                                                                                                                                                                                                  |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Created  | Export task creation date                                                                                                                                                                                                                                                                                                                                                    |
| Type     | <p>Type of data:</p><ul><li>Users</li><li>Devices</li><li>Sessions</li></ul>                                                                                                                                                                                                                                                                                                 |
| From     | Start date of the export period                                                                                                                                                                                                                                                                                                                                              |
| Till     | End date of the export period                                                                                                                                                                                                                                                                                                                                                |
| Status   | <p>Export status:</p><ul><li><strong>In progress</strong> - a data export task in awaiting completion</li><li><strong>Done</strong> - the process of data export is finished</li><li><strong>No data</strong> - the Platform cannot find any data corresponding to the filter parameters</li><li><strong>Failed</strong> - technical issue, contact us for details</li></ul> |
| Download | Link on CSV file to download                                                                                                                                                                                                                                                                                                                                                 |

## Actions

Select what type of data is going to be exported by clicking on "**Add**" button and choosing one option at a time.

![Export data types selection menu](../.gitbook/assets/select\_type\_data\_export.png)

A new export task will be created with "**In **_****_** progress**" status and displayed in the list. When processing of the task is complete, the status will change to either "**Done**", "**Failed**" or "**No Data**". In case of success, the link to the export file will appear in the "**Download**" column.

{% hint style="info" %}
Failed tasks can be restarted
{% endhint %}

#### **Exporting Sessions**

To export session data, a date range must be selected. You can choose the range manually or use a preset (Today, This week, This month, Yesterday, Last week or Last month). &#x20;

![Sessions data export date picker](../.gitbook/assets/export\_sessions.png)
