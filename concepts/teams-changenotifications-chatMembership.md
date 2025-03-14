---
title: "Get change notifications for chat membership using Microsoft Graph"
description: "Learn how to get notifications for changes for chat membership using Microsoft Graph APIs."
author: "RamjotSingh"
ms.localizationpriority: high
ms.prod: "microsoft-teams"
ms.custom: scenarios:getting-started
---

# Get change notifications for chat membership using Microsoft Graph

Change notifications enable you to subscribe to changes (create and delete) in chats membership. You can get notified whenever a member is added or removed from a chat. You can also get the resource data in the notifications and therefore avoid calling the API to get the payload.

## Subscribe to changes in membership of any chat at tenant level

To get change notifications for membership changes in any chat across the tenant, subscribe to `/chats/getAllMembers`. This resource supports [including resource data](webhooks-with-resource-data.md) in the notification.

[!INCLUDE [teams-model-A-and-B-disclaimer](../includes/teams-model-A-and-B-disclaimer.md)]

### Permissions

|Permission type      | Permissions (from least to most privileged)              | Supported versions |
|:--------------------|:---------------------------------------------------------|:-------------------|
|Delegated (work or school account) | Not supported. | Not supported. |
|Delegated (personal Microsoft account) | Not supported.    | Not supported. |
|Application | ChatMember.Read.All, ChatMember.ReadWrite.All, Chat.ReadBasic.All, Chat.Read.All, Chat.ReadWrite.All  | beta|

### Example

```http
POST https://graph.microsoft.com/beta/subscriptions
Content-Type: application/json

{
  "changeType": "created,deleted",
  "notificationUrl": "https://webhook.azurewebsites.net/api/resourceNotifications",
  "resource": "/chats/getAllMembers",
  "includeResourceData": true,
  "encryptionCertificate": "{base64encodedCertificate}",
  "encryptionCertificateId": "{customId}",
  "expirationDateTime": "2019-09-19T11:00:00.0000000Z",
  "clientState": "{secretClientState}"
}
```

## Subscribe to changes in membership of a particular chat

To get change notifications for membership changes in a particular chat, subscribe to `/chats/{id}/members`. This resource supports [including resource data](webhooks-with-resource-data.md) in the notification.

### Permissions

|Permission type      | Permissions (from least to most privileged)              | Supported versions |
|:--------------------|:---------------------------------------------------------|:-------------------|
|Delegated (work or school account) | ChatMember.Read, ChatMember.ReadWrite, Chat.ReadBasic, Chat.Read, Chat.ReadWrite | beta |
|Delegated (personal Microsoft account) | Not supported.    | Not supported. |
|Application | ChatMember.Read.Chat*, Chat.Manage.Chat*, ChatMember.Read.All, ChatMember.ReadWrite.All, Chat.ReadBasic.All, Chat.Read.All, Chat.ReadWrite.All  | beta |

> **Note**: Permissions marked with * use [resource-specific consent]( https://aka.ms/teams-rsc).

### Example

```http
POST https://graph.microsoft.com/beta/subscriptions
Content-Type: application/json

{
  "changeType": "created,deleted",
  "notificationUrl": "https://webhook.azurewebsites.net/api/resourceNotifications",
  "resource": "/chats/{id}/members",
  "includeResourceData": true,
  "encryptionCertificate": "{base64encodedCertificate}",
  "encryptionCertificateId": "{customId}",
  "expirationDateTime": "2019-09-19T11:00:00.0000000Z",
  "clientState": "{secretClientState}"
}
```



### Notifications with resource data

For notifications with resource data, the payload looks like the following. This payload is for a membership change in a chat.

```json
{
    "value": [{
        "subscriptionId": "c0125ef2-7a87-4e94-aa71-b995510f369b",
		"changeType": "Created",
		"clientState": "<<--SpecifiedClientState-->>",
		"subscriptionExpirationDateTime": "2021-06-03T11:04:58.5537601+00:00",
		"resource": "chats('19:1273a016-201d-4f95-8083-1b7f99b3edeb_976f4b31-fd01-4e0b-9178-29cc40c14438@unq.gbl.spaces')/members('MCMjMjQzMmI1N2ItMGFiZC00M2RiLWFhN2ItMTZlYWRkMTE1ZDM0IyMxOToxMjczYTAxNi0yMDFkLTRmOTUtODA4My0xYjdmOTliM2VkZWJfOTc2ZjRiMzEtZmQwMS00ZTBiLTkxNzgtMjljYzQwYzE0NDM4QHVucS5nYmwuc3BhY2VzIyMyZmM2MDY2My0xOWEyLTRhYTQtODUyYy1mN2JhNGU5MGFkYTI=')",
		"resourceData": {
			"id": "MCMjMjQzMmI1N2ItMGFiZC00M2RiLWFhN2ItMTZlYWRkMTE1ZDM0IyMxOToxMjczYTAxNi0yMDFkLTRmOTUtODA4My0xYjdmOTliM2VkZWJfOTc2ZjRiMzEtZmQwMS00ZTBiLTkxNzgtMjljYzQwYzE0NDM4QHVucS5nYmwuc3BhY2VzIyMyZmM2MDY2My0xOWEyLTRhYTQtODUyYy1mN2JhNGU5MGFkYTI=",
			"@odata.type": "#microsoft.graph.aadUserConversationMember",
			"@odata.id": "chats('19:1273a016-201d-4f95-8083-1b7f99b3edeb_976f4b31-fd01-4e0b-9178-29cc40c14438@unq.gbl.spaces')/members('MCMjMjQzMmI1N2ItMGFiZC00M2RiLWFhN2ItMTZlYWRkMTE1ZDM0IyMxOToxMjczYTAxNi0yMDFkLTRmOTUtODA4My0xYjdmOTliM2VkZWJfOTc2ZjRiMzEtZmQwMS00ZTBiLTkxNzgtMjljYzQwYzE0NDM4QHVucS5nYmwuc3BhY2VzIyMyZmM2MDY2My0xOWEyLTRhYTQtODUyYy1mN2JhNGU5MGFkYTI=')"
		},
		"EncryptedContent": {
			"data": "<<--EncryptedContent-->>",
			"dataKey": "<<--EnryptedDataKeyUsedForEncryptingContent-->>",
			"encryptionCertificateId": "<<--IdOfTheCertificateUsedForEncryptingDataKey-->>",
			"encryptionCertificateThumbprint": "<<--ThumbprintOfTheCertificateUsedForEncryptingDataKey-->>"
		},
        "tenantId": "<<--TenantForWhichNotificationWasSent-->>"
    }],
    "validationTokens": ["<<--ValidationTokens-->>"]
}
```

For details about how to validate tokens and decrypt the payload, see [Set up change notifications that include resource data](webhooks-with-resource-data.md).

The decrypted notification payload looks like the following. The payload conforms to the [aaduserconversationmember](/graph/api/resources/aaduserconversationmember?preserve-view=true) schema. The payload is similar to that returned by GET operations.

```json
{
    "userId": "2fc60663-19a2-4aa4-852c-f7ba4e90ada2",
	"email": null,
	"tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
	"id": "MCMjMjQzMmI1N2ItMGFiZC00M2RiLWFhN2ItMTZlYWRkMTE1ZDM0IyMxOToxMjczYTAxNi0yMDFkLTRmOTUtODA4My0xYjdmOTliM2VkZWJfOTc2ZjRiMzEtZmQwMS00ZTBiLTkxNzgtMjljYzQwYzE0NDM4QHVucS5nYmwuc3BhY2VzIyMyZmM2MDY2My0xOWEyLTRhYTQtODUyYy1mN2JhNGU5MGFkYTI=",
	"roles": [
	"Owner"
	],
	"displayName": null,
	"visibleHistoryStartDateTime": "1970-01-01T00:00:00Z",
	"user": null
}
```

### Notifications without resource data

The following payload describes the information sent in the request for notifications without resource data. This particular payload signifies that a user has been added to a chat.

```json
{
    "subscriptionId": "cae901f1-ad1d-41b1-95b7-37029ed327bf",
	"changeType": "Created",
	"tenantId": "<<--TenantForWhichNotificationWasSent-->>",
	"clientState": "<<--SpecifiedClientState-->>",
	"subscriptionExpirationDateTime": "2021-06-03T10:58:54.7656077+00:00",
	"resource": "chats('19:1273a016-201d-4f95-8083-1b7f99b3edeb_976f4b31-fd01-4e0b-9178-29cc40c14438@unq.gbl.spaces')/members('MCMjMjQzMmI1N2ItMGFiZC00M2RiLWFhN2ItMTZlYWRkMTE1ZDM0IyMxOToxMjczYTAxNi0yMDFkLTRmOTUtODA4My0xYjdmOTliM2VkZWJfOTc2ZjRiMzEtZmQwMS00ZTBiLTkxNzgtMjljYzQwYzE0NDM4QHVucS5nYmwuc3BhY2VzIyMyZmM2MDY2My0xOWEyLTRhYTQtODUyYy1mN2JhNGU5MGFkYTI=')",
	"resourceData": {
		"id": "MCMjMjQzMmI1N2ItMGFiZC00M2RiLWFhN2ItMTZlYWRkMTE1ZDM0IyMxOToxMjczYTAxNi0yMDFkLTRmOTUtODA4My0xYjdmOTliM2VkZWJfOTc2ZjRiMzEtZmQwMS00ZTBiLTkxNzgtMjljYzQwYzE0NDM4QHVucS5nYmwuc3BhY2VzIyMyZmM2MDY2My0xOWEyLTRhYTQtODUyYy1mN2JhNGU5MGFkYTI=",
		"@odata.type": "#microsoft.graph.aadUserConversationMember",
		"@odata.id": "chats('19:1273a016-201d-4f95-8083-1b7f99b3edeb_976f4b31-fd01-4e0b-9178-29cc40c14438@unq.gbl.spaces')/members('MCMjMjQzMmI1N2ItMGFiZC00M2RiLWFhN2ItMTZlYWRkMTE1ZDM0IyMxOToxMjczYTAxNi0yMDFkLTRmOTUtODA4My0xYjdmOTliM2VkZWJfOTc2ZjRiMzEtZmQwMS00ZTBiLTkxNzgtMjljYzQwYzE0NDM4QHVucS5nYmwuc3BhY2VzIyMyZmM2MDY2My0xOWEyLTRhYTQtODUyYy1mN2JhNGU5MGFkYTI=')"
	}
}
```

The **resource** and **@odata.id** properties can be used to make calls to Microsoft Graph to get the payload for the chat member details. GET calls will always return the current state of the chat member details. If the chat member details has changed between when the notification is sent and when the chat member details were retrieved, the operation will return the updated chat member details.

## See also
- [Microsoft Graph change notifications](webhooks.md)
- [Microsoft Teams API overview](teams-concept-overview.md)
