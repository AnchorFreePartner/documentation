---
description: Find out how to create custom or choose exiting pools for your project
---

# Pools

## Overview

![Pool page overview](../../../.gitbook/assets/screenshot-2021-06-02-at-15.57.16.png)

| Parameter | Description |
| :--- | :--- |
| ![](../../../.gitbook/assets/checkbox.webp) | to enable \(make it usable\) a specific pool |
| Type | to represent pool's type \(either **Public** or **Private**\) |
| Name | to identify the pool with **unique** text label |
| Permissions | to specify which projects can **read**, **write**, **list** or **use** a pool |
| Description | to provide extra information on pool \(optional\) |

{% hint style="info" %}
You can have a JSON representation of pool's settings by hovering the "Permissions" column and copy the text inside the tooltip
{% endhint %}

![JSON representation of pool permissions](../../../.gitbook/assets/screenshot-2021-06-02-at-15.57.23.png)

## Actions

### Add

![New pool dialog](../../../.gitbook/assets/screenshot-2021-06-02-at-16.49.34.png)

{% hint style="warning" %}
New pools are created **Public** by default. It's currently unavailable to change the type manually.
{% endhint %}

![](../../../.gitbook/assets/screenshot-2021-06-02-at-16.49.41.png)

![](../../../.gitbook/assets/screenshot-2021-06-02-at-16.50.17.png)

{% hint style="danger" %}
Pool name is a unique identifier; attempting to use an existing name will result in an error "**Pool already exists"** and your pool will not be created.
{% endhint %}

![](../../../.gitbook/assets/screenshot-2021-06-02-at-16.50.49.png)

### Copy

Any pool from the list can be copied fully \(including type\). The name of the pool will be added with a postfix representing current time in [unix epoch format](https://en.wikipedia.org/wiki/Unix_time) \(e.g. _\_1622643592669_\).

### Edit

The edit screen repeats the add screen in terms of both the set of fields and the logic.

### Delete



