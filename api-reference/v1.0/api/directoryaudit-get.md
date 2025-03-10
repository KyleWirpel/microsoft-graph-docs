---
title: "Get directoryAudit"
description: "Describes the get method of the directoryAudit resource (entity) from the Microsoft Graph API."
ms.localizationpriority: medium
author: "SarahBar"
ms.prod: "identity-and-access-reports"
doc_type: apiPageType
---

# Get directoryAudit

Namespace: microsoft.graph

Get a specific Azure Active Directory audit log item. This includes an audit log item generated by various services within Azure Active Directory like user, application, device and group management, privileged identity management (PIM), access reviews, terms of use, identity protection, password management (self-service and admin password resets), self-service group management, and so on.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type      | Permissions (from least to most privileged)              |
|:--------------------|:---------------------------------------------------------|
|Delegated (work or school account) | AuditLog.Read.All and Directory.Read.All |
|Delegated (personal Microsoft account) | Not supported   |
|Application | AuditLog.Read.All and Directory.Read.All |

> [!IMPORTANT]
> This API has a [known issue](/graph//graph/known-issues#license-check-errors-for-azure-ad-activity-reports) and currently requires consent to both the **AuditLog.Read.All** and **Directory.Read.All** permissions.

## HTTP request

<!-- { "blockType": "ignored" } -->
```http
GET /auditLogs/directoryAudits/{id}
```

## Optional query parameters

This method supports OData query parameters to help customize the response. For details about how to use these parameters, see [OData query parameters](/graph/query-parameters).

## Request headers

| Name      |Description|
|:----------|:----------|
| Authorization  | Bearer {code}|

## Request body

Do not supply a request body for this method.

## Response

If successful, this method returns a `200 OK` response code and [directoryAudit](../resources/directoryaudit.md) object in the response body.

## Example

### Request

Here is an example of the request.

# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "get_directoryaudit_1"
}-->

```msgraph-interactive
GET https://graph.microsoft.com/v1.0/auditLogs/directoryAudits/{id}
```
# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/get-directoryaudit-1-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/get-directoryaudit-1-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Objective-C](#tab/objc)
[!INCLUDE [sample-code](../includes/snippets/objc/get-directoryaudit-1-objc-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/get-directoryaudit-1-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Go](#tab/go)
[!INCLUDE [sample-code](../includes/snippets/go/get-directoryaudit-1-go-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---


### Response

Here is an example of the response.
>**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.directoryAudit"
} -->

```http
HTTP/1.1 200 OK
Content-type: application/json

{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#auditlogs/directoryaudits",
  "value": [{
		"id": "id",
		"category": "UserManagement",
		"correlationId": "da159bfb-54fa-4092-8a38-6e1fa7870e30",
		"result": "success",
		"resultReason": "Successfully added member to group",
		"activityDisplayName": "Add member to group",
		"activityDateTime": "2018-01-09T21:20:02.7215374Z",
		"loggedByService": "Core Directory",
		"initiatedBy": {
			"user": {
				"id": "728309ae-1a37-4937-9afe-e35d964db09b",
				"displayName": "Audry Oliver",
				"userPrincipalName": "bob@wingtiptoysonline.com",
				"ipAddress": "127.0.0.1"
			},
			"app": null
		},
		"targetResource": [{
			"id": "ef7e527d-6c92-4234-8c6d-cf6fdfb57f95",
			"displayName": "Example.com",
			"Type": "Group",
			"modifiedProperties": [{
				"displayName": "Action Client Name",
				"oldValue": null,
				"newValue": "DirectorySync" 
			}],
			"groupType": "unifiedGroups"
		}, {
			"id": "1f0e98f5-3161-4c6b-9b50-d488572f2bb7",
			"displayName": null,
			"Type": "User",
			"modifiedProperties": [],
			"userPrincipalName": "example@contoso.com"
		}],
		"additionalDetails": [{
			"key": "Additional Detail Name",
			"value": "Additional Detail Value"
		}]
	}]
}
```

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "Get directoryAudits",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": [
  ]
}-->

