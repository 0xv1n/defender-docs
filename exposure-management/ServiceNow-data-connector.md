---
title: Integrate ServiceNow data connector in Microsoft Security Exposure Management
description: Learn how to the ServiceNow data connector in Microsoft Security Exposure Management.
ms.author: dlanger
author: dlanger
manager: rayne-wiselman
ms.topic: overview
ms.service: exposure-management
ms.date: 09/24/2024
---

# ServiceNow data connector

To set up the ServiceNow integration, you need the hostname of your ServiceNow instance, such as “contoso.service-now.com”. The connector authenticates with Basic Auth using username and password for read only access.

## ServiceNow configuration

1. Create a New ServiceNow user:
   1. Follow the steps [here](https://docs.servicenow.com/en-US/bundle/vancouver-platform-administration/page/administer/users-and-groups/task/t_CreateAUser.html) to create a new user.
   2. Keep the **username (User Id) and password** you provided for future use.
   3. If there’s no password field, submit the form to create the user. Afterwards, when you select on the new user, you receive the **Set Password** option.
   4. Check the **Web service access only** box.
2. Assign a **cmdb_read** role to the user you have created. Detailed instructions can be found [here](https://docs.servicenow.com/bundle/vancouver-platform-administration/page/administer/users-and-groups/task/t_AssignARoleToAUser.html).

> **Note:** The ServiceNow connector only supports Basic Authentication. OAuth authentication will be made available at a later time.

## Establish ServiceNow connection in Exposure Management

To establish a connection with ServiceNow in Exposure Management, follow these steps:

1. Open the [Data Connectors](https://security.microsoft.com/exposure-data-connectors) from the Exposure Management navigation and select **Connect** in the ServiceNow CMDB tile.
1. Enter your ServiceNow instance **details** (created in the ServiceNow configuration) and select **Connect**.

## Retrieved data

Exposure Management currently retrieves data on devices, their business application association, and business criticality. Additional data is also retrieved that helps identify the device, such as network adapter information and OS data.

The following fields are ingested via the connector:

 **Devices**:

- properties
  - os
  - osVersion
  - osServicePack
  - cpuType
  - category
  - assetTag
  - virtual
  - serviceNowCriticality
  - usedFor
  - networkAdapters
  - lastLoggedOnUser
  - mostFrequentUser
  - sysClassName
  - uPrimaryBusinessApplication

**networkAdapter**:

- properties:
  - name
  - sysId
  - macAddress
  - ipAddress
  - ipDefaultGateway

 **businessApplication**:

- properties:
  - sysId
  - number
  - uCriticality
  - businessCriticality

## Troubleshooting the connector

Some common issues that might come up when configuring the ServiceNow CMDB connector.

### 'The remote server name could not be resolved'

Verify ServiceNow Instance hostname.
Learn more about authentication to ServiceNow here: [Authentication (servicenow.com)](https://docs.servicenow.com/bundle/vancouver-platform-security/page/integrate/single-sign-on/concept/c_Authentication.html)

### 429 (Too Many Requests)

The system periodically pulls data from the configured external providers, which may have a limit on the number of concurrent requests.
We recommend creating a dedicated user or account for the connector to avoid reaching this limit.

### 'Temporary disconnected' or 'Temporary failure' error

In cases where the error message indicates this is a temporary issue, check again later to see if the issue was auto resolved.
Note: in some cases the issue will not be auto resolved and manual user intervention is required. if an elaborated error message is shown, please act accordingly. otherwise, please contact Support

### Not seeing ServiceNow CMDB CIs in the ingested data

See [Retrieved data](#retrieved-data) for a description of the  data expected to be retrieved by the ServiceNow CMDB connector.
If there's still missing data, please contact Support.

### Configure ServiceNow allowed IPs to enable Exposure Management connectors to access ServiceNow

Read how to add the set of IPs to add to your allowlist here: [Allowlist IP addresses](configure-data-connectors.md#allowlist-ip-addresses)

### Unable to connect/disconnect

If you encounter an error message indicating there was an error connecting / disconnecting. Try again in a few minutes. If the issue persists, please contact Support.

## Next steps

[Getting value from your data connectors](value-data-connectors.md).
