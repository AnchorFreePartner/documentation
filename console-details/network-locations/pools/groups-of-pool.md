---
description: Take a look on the rule composition of the pool
---

# Groups of pool

## Overview

![Pool rules page](../../../.gitbook/assets/screenshot-2021-06-02-at-15.57.52.png)

This interface provides functionality for viewing and managing server location selection rules \(server selector\) depending on the client location \(request selector\).

| Parameter | Description |
| :--- | :--- |
| \# | a sequential number of the table entry |
| Rule name | a unique text identifier |
| Priority | lower value is processed first |
| Request selector | client location condition |
| Server selector | selected server location value |
| Description | extra information on the rule \(optional\) |

{% hint style="info" %}
You can have a JSON representation of request selector by hovering a field in the "**Request selector**" column and copy the text inside the tooltip
{% endhint %}

![Request selector JSON representation](../../../.gitbook/assets/screenshot-2021-06-02-at-15.58.35.png)

{% hint style="info" %}
You can get a JSON representation of server selector by hovering a field in the "**Server selector**" column and copy the text inside the tooltip
{% endhint %}

![Server selector JSON representation](../../../.gitbook/assets/screenshot-2021-06-02-at-15.58.44.png)

## Actions

### Add

You can add a rule to the pool by clicking the "**Add**" button in the upper right corner; the corresponding dialog box will appear:

![](../../../.gitbook/assets/screenshot-2021-06-02-at-20.25.58.png)

| Parameter | Description |
| :--- | :--- |
| Rule name |  |
| Rule selector |  |
| Server selector |  |
| Description |  |
| Priority |  |

### Edit

### Delete

