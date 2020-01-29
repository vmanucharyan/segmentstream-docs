---
layout: page
section: datasources
title: "retailCRM"
order: 1
---

In this section you will learn:
* How to connect retailCRM data import.

> Attention! The [Google BigQuery](/integrations/google-bigquery) integration has to be enabled to use this feature.

### Page contents
------
<ul class="page-navigation">
  <li><a href="#importing-data">Importing data from retailCRM</a></li>
  <li><a href="#connecting-and-configuring">Connecting and configuring</a></li>
  <li><a href="#options-description">Options description</a></li>
  <li><a href="#display-name">Display name</a></li>
  <li><a href="#retailcrm-subdomain">retailCRM subdomain</a></li>
  <li><a href="#orders-import">Orders import</a></li>
  <li><a href="#saving-disconnecting-disabling">Saving, Disconnecting, Disabling data source</a></li>
  <li><a href="#where-to-get-orders-data">Where to get orders data</a></li>
</ul>

### <a name="importing-data"></a>Importing data from retailCRM
------

After enabling this data source, retailCRM data will be uploaded to BigQuery once every 24 hours.

### <a name="connecting-and-configuring"></a>Connecting and configuring
------
Before connecting the data source, you must create an API key, this is described in detail in the [retailCRM docs](https://help.retailcrm.ru/Users/ApiKeys).

The process of connecting data sources is described in detail in the [overview](/datasources/index).

After authorization you need to set the data source parameters.

### <a name="options-description"></a>Options description
------
![](/img/retailcrm.png)

### <a name="display-name"></a>Display name
The name of the data source. It is displayed in the interface in the list of sources.

### <a name="retailcrm-subdomain"></a>retailCRM subdomain
Should be filled with the first part of your CRM address. For example, if your CRM address is https://test-account.retailcrm.ru/, then the subdomain will be "test-account".

### <a name="orders-import"></a>Orders import
Enable import of orders data. If this option enabled, updated orders for the previous day will be uploaded.

### <a name="saving-disconnecting-disabling"></a>Saving, Disconnecting, Disabling data source
To save and enable the data source, click **Save**.

The **Disconnect** button is used to revoke the authorization data. The settings are saved.

You can enable or disable the data source at any time by using the switch on the top right.

### <a name="where-to-get-orders-data"></a>Where to get orders data
- **retailCrmOrders_{YYYYMMDD}** - data for updated "Orders"