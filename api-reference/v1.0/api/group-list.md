---
title: "List groups"
description: "List all the groups available in an organization, including but not limited to Microsoft 365 groups."
ms.localizationpriority: high
author: "Jordanndahl"
ms.prod: "groups"
doc_type: apiPageType
---

# List groups

Namespace: microsoft.graph

List all the groups in an organization, including but not limited to Microsoft 365 groups. 

This operation returns by default only a subset of the properties for each group. These default properties are noted in the [Properties](../resources/group.md#properties) section. To get properties that are _not_ returned by default, do a [GET](group-get.md) operation for the group and specify the properties in a `$select` OData query option. The **hasMembersWithLicenseErrors** property is an exception and is not returned in the `$select` query.

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type      | Permissions (from least to most privileged)              |
|:--------------------|:---------------------------------------------------------|
|Delegated (work or school account) | GroupMember.Read.All, Group.Read.All, Directory.Read.All, Group.ReadWrite.All, Directory.ReadWrite.All, Directory.AccessAsUser.All |
|Delegated (personal Microsoft account) | Not supported.    |
|Application | GroupMember.Read.All, Group.Read.All, Directory.Read.All, Group.ReadWrite.All, Directory.ReadWrite.All |

## HTTP request
<!-- { "blockType": "ignored" } -->
```http
GET /groups
```

## Optional query parameters
This method supports the `$count`, `$expand`, `$filter`, `$orderBy`, `$search`, `$select`, and `$top` [OData query parameters](/graph/query-parameters) to help customize the response. The default and maximum page sizes are 100 and 999 group objects respectively. Some queries are supported only when you use the **ConsistencyLevel** header set to `eventual` and `$count`. For more information, see [Advanced query capabilities on Azure AD directory objects](/graph/aad-advanced-queries).

To list only Microsoft 365 groups (aka unified groups), apply a filter on **groupTypes**:
<!-- { "blockType": "ignored" } -->
```http
GET https://graph.microsoft.com/v1.0/groups?$filter=groupTypes/any(c:c+eq+'Unified')
```

The `$search` query parameter supports tokenization only on the **displayName** and **description** fields and requires the **ConsistencyLevel** header. Fields other than **displayName** and **description** default to `$filter` `startswith` behavior.

For more information on OData query options, see [OData query parameters](/graph/query-parameters). For more information about the use of **ConsistencyLevel** and `$count`, see [Advanced query capabilities on Azure AD directory objects](/graph/aad-advanced-queries).

## Request headers

| Name | Description |
|:---- |:----------- |
| Authorization  | Bearer {token}. Required. |
| ConsistencyLevel | eventual. This header and `$count` are required when using `$search`, or in specific usage of `$filter`. For more information about the use of **ConsistencyLevel** and `$count`, see [Advanced query capabilities on Azure AD directory objects](/graph/aad-advanced-queries). |

## Request body
Do not supply a request body for this method.

## Response
If successful, this method returns a `200 OK` response code and collection of [group](../resources/group.md) objects in the response body. The response includes only the default properties of each group.

## Examples

### Example 1: Get a list of groups

#### Request

The following is an example of the request.


# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "get_groups"
}-->
```msgraph-interactive
GET https://graph.microsoft.com/v1.0/groups
```
# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/get-groups-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/get-groups-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Objective-C](#tab/objc)
[!INCLUDE [sample-code](../includes/snippets/objc/get-groups-objc-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/get-groups-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Go](#tab/go)
[!INCLUDE [sample-code](../includes/snippets/go/get-groups-go-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---


#### Response

The following is an example of the response.

>**Note:** The response object shown here might be shortened for readability. All the default properties are returned for each group in an actual call.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.group",
  "isCollection": true
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json

{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#groups",
  "value": [
    {
      "id": "45b7d2e7-b882-4a80-ba97-10b7a63b8fa4",
      "deletedDateTime": null,
      "classification": null,
      "createdDateTime": "2018-12-22T02:21:05Z",
      "description": "Self help community for golf",
      "displayName": "Golf Assist",
      "expirationDateTime": null,
      "groupTypes": [
        "Unified"
      ],
      "isAssignableToRole": null,
      "mail": "golfassist@contoso.com",
      "mailEnabled": true,
      "mailNickname": "golfassist",
      "membershipRule": null,
      "membershipRuleProcessingState": null,
      "onPremisesLastSyncDateTime": null,
      "onPremisesSecurityIdentifier": null,
      "onPremisesSyncEnabled": null,
      "preferredDataLocation": "CAN",
      "preferredLanguage": null,
      "proxyAddresses": [
        "smtp:golfassist@contoso.onmicrosoft.com",
        "SMTP:golfassist@contoso.com"
      ],
      "renewedDateTime": "2018-12-22T02:21:05Z",
      "resourceBehaviorOptions": [],
      "resourceProvisioningOptions": [],
      "securityEnabled": false,
      "theme": null,
      "visibility": "Public",
      "onPremisesProvisioningErrors": []
    },
    {
      "id": "d7797254-3084-44d0-99c9-a3b5ab149538",
      "deletedDateTime": null,
      "classification": null,
      "createdDateTime": "2018-11-19T20:29:40Z",
      "description": "Talk about golf",
      "displayName": "Golf Discussion",
      "expirationDateTime": null,
      "groupTypes": [],
      "isAssignableToRole": null,
      "mail": "golftalk@contoso.com",
      "mailEnabled": true,
      "mailNickname": "golftalk",
      "membershipRule": null,
      "membershipRuleProcessingState": null,
      "onPremisesLastSyncDateTime": null,
      "onPremisesSecurityIdentifier": null,
      "onPremisesSyncEnabled": null,
      "preferredDataLocation": "CAN",
      "preferredLanguage": null,
      "proxyAddresses": [
        "smtp:golftalk@contoso.onmicrosoft.com",
        "SMTP:golftalk@contoso.com"
      ],
      "renewedDateTime": "2018-11-19T20:29:40Z",
      "resourceBehaviorOptions": [],
      "resourceProvisioningOptions": [],
      "securityEnabled": false,
      "theme": null,
      "visibility": null,
      "onPremisesProvisioningErrors": []
    }
  ]
}
```

### Example 2: Get a filtered list of groups including the count of returned objects

The following is an example of the request. This request requires the **ConsistencyLevel** header set to `eventual` because `$count` is in the request. For more information about the use of **ConsistencyLevel** and `$count`, see [Advanced query capabilities on Azure AD directory objects](/graph/aad-advanced-queries).

>**Note:** The `$count` and `$search` query parameters are currently not available in Azure AD B2C tenants.

#### Request


# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "get_groups_withlicenseerrors_count"
}-->
```msgraph-interactive
GET https://graph.microsoft.com/v1.0/groups?$count=true&$filter=hasMembersWithLicenseErrors+eq+true&$select=id,displayName
ConsistencyLevel: eventual
```
# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/get-groups-withlicenseerrors-count-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/get-groups-withlicenseerrors-count-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Objective-C](#tab/objc)
[!INCLUDE [sample-code](../includes/snippets/objc/get-groups-withlicenseerrors-count-objc-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/get-groups-withlicenseerrors-count-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Go](#tab/go)
[!INCLUDE [sample-code](../includes/snippets/go/get-groups-withlicenseerrors-count-go-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---


#### Response

The following is an example of the response which includes only the requested properties.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.group",
  "isCollection": true
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json

{
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#groups(id,displayName)",
   "@odata.count":2,
   "value":[
      {
         "id":"11111111-2222-3333-4444-555555555555",
         "displayName":"Contoso Group 1"
      },
      {
         "id":"22222222-3333-4444-5555-666666666666",
         "displayName":"Contoso Group 2"
      }
   ]
}
```

### Example 3: Get only a count of groups

#### Request

The following is an example of the request. This request requires the **ConsistencyLevel** header set to `eventual` because `$count` is in the request. For more information about the use of **ConsistencyLevel** and `$count`, see [Advanced query capabilities on Azure AD directory objects](/graph/aad-advanced-queries).

>**Note:** The `$count` and `$search` query parameters are currently not available in Azure AD B2C tenants.

<!-- {
  "blockType": "ignored",
  "name": "get_count_only"
  }-->
```msgraph-interactive
GET https://graph.microsoft.com/v1.0/groups/$count
ConsistencyLevel: eventual
```

#### Response

The following is an example of the response.

<!-- {
  "blockType": "response"
} -->
```http
HTTP/1.1 200 OK
Content-type: text/plain

893
```

### Example 4: Use $filter and $top to get one group with a display name that starts with 'a' including a count of returned objects

#### Request

The following is an example of the request. This request requires the **ConsistencyLevel** header set to `eventual` and the `$count=true` query string because the request has both the `$orderBy` and `$filter` query parameters. For more information about the use of **ConsistencyLevel** and `$count`, see [Advanced query capabilities on Azure AD directory objects](/graph/aad-advanced-queries).

>**Note:** The `$count` and `$search` query parameters are currently not available in Azure AD B2C tenants.


# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "get_a_count"
}-->
```msgraph-interactive
GET https://graph.microsoft.com/v1.0/groups?$filter=startswith(displayName, 'a')&$count=true&$top=1&$orderby=displayName
ConsistencyLevel: eventual
```
# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/get-a-count-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/get-a-count-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Objective-C](#tab/objc)
[!INCLUDE [sample-code](../includes/snippets/objc/get-a-count-objc-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/get-a-count-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Go](#tab/go)
[!INCLUDE [sample-code](../includes/snippets/go/get-a-count-go-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---


#### Response

The following is an example of the response.

>**Note:** The response object shown here might be shortened for readability.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.group",
  "isCollection": true
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json

{
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#groups",
   "@odata.count":1,
   "value":[
      {
         "displayName":"a",
         "mailNickname":"a241"
      }
   ]
}
```

### Example 5: Use $search to get groups with display names that contain the letters 'Video' including a count of returned objects

#### Request

The following is an example of the request. This request requires the **ConsistencyLevel** header set to `eventual` because `$search` is in the request. For more information about the use of **ConsistencyLevel** and `$count`, see [Advanced query capabilities on Azure AD directory objects](/graph/aad-advanced-queries).

>**Note:** The `$count` and `$search` query parameters are currently not available in Azure AD B2C tenants.

<!-- {
  "blockType": "request",
  "name": "get_video_count"
}-->
```msgraph-interactive
GET https://graph.microsoft.com/v1.0/groups?$search="displayName:Video"&$count=true
ConsistencyLevel: eventual
```

#### Response

The following is an example of the response.

>**Note:** The response object shown here might be shortened for readability.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.group",
  "isCollection": true
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json

{
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#groups",
   "@odata.count":1396,
   "value":[
      {
         "displayName":"SFA Videos",
         "mail":"SFAVideos@service.contoso.com",
         "mailNickname":"SFAVideos"
      }
   ]
}
```

### Example 6: Use $search to get groups with display names that contain the letters 'Video' or a description that contains the letters 'prod' including a count of returned objects

#### Request

The following is an example of the request. This request requires the **ConsistencyLevel** header set to `eventual` because `$search` is in the request. For more information about the use of **ConsistencyLevel** and `$count`, see [Advanced query capabilities on Azure AD directory objects](/graph/aad-advanced-queries).

>**Note:** The `$count` and `$search` query parameters are currently not available in Azure AD B2C tenants.

<!-- {
  "blockType": "request",
  "name": "get_video_count"
}-->
```msgraph-interactive
GET https://graph.microsoft.com/v1.0/groups?$search="displayName:Video" OR "description:prod"&$orderby=displayName&$count=true
ConsistencyLevel: eventual
```

#### Response

The following is an example of the response.

>**Note:** The response object shown here might be shortened for readability.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.group",
  "isCollection": true
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json

{
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#groups",
   "@odata.count":1396,
   "value":[
      {
         "displayName":"SFA Videos",
         "mail":"SFAVideos@service.contoso.com",
         "mailNickname":"SFAVideos"
      },
      {
         "description":"Video Production",
         "displayName":"Video Production",
         "mail":"videoprod@service.contoso.com",
         "mailNickname":"VideoProduction"
      }
   ]
}
```

### Example 7: List dynamic security groups

#### Request

The following is an example of the request that filters by the **membershipRuleProcessingState** to retrieve dynamic groups. You may also filter by the **groupTypes** properties (that is, `$filter=groupTypes/any(s:s eq 'DynamicMembership')`). This request requires the **ConsistencyLevel** header set to `eventual` and the `$count=true` query string because the request uses the `not` operator of the `$filter` query parameter. For more information about the use of **ConsistencyLevel** and `$count`, see [Advanced query capabilities on Azure AD directory objects](/graph/aad-advanced-queries).

>**Note:** The `$count` and `$search` query parameters are currently not available in Azure AD B2C tenants.



# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "get_enabled_dynamic_groups"
}-->
```msgraph-interactive
GET https://graph.microsoft.com/v1.0/groups?$filter=mailEnabled eq false and securityEnabled eq true and NOT(groupTypes/any(s:s eq 'Unified')) and membershipRuleProcessingState eq 'On'&$count=true&$select=id,membershipRule,membershipRuleProcessingState
ConsistencyLevel: eventual
```
# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/get-enabled-dynamic-groups-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/get-enabled-dynamic-groups-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Objective-C](#tab/objc)
[!INCLUDE [sample-code](../includes/snippets/objc/get-enabled-dynamic-groups-objc-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/get-enabled-dynamic-groups-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Go](#tab/go)
[!INCLUDE [sample-code](../includes/snippets/go/get-enabled-dynamic-groups-go-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---



#### Response

The following is an example of the response.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.group",
  "isCollection": true
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#groups(id,membershipRule,membershipRuleProcessingState)",
    "@odata.count": 1,
    "value": [
        {
            "@odata.id": "https://graph.microsoft.com/v2/84841066-274d-4ec0-a5c1-276be684bdd3/directoryObjects/e9f4a701-e7b5-4401-a0ca-5bd5f3cdcf4b/Microsoft.DirectoryServices.Group",
            "id": "e9f4a701-e7b5-4401-a0ca-5bd5f3cdcf4b",
            "membershipRule": "(user.userType -contains \"Guest\" and user.accountEnabled -eq true) or (user.city -eq \"Nairobi\")",
            "membershipRuleProcessingState": "On"
        }
    ]
}
```

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "List groups",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": [
  ]
}-->

