---
title: "Get a user"
description: "Retrieve the properties and relationships of user object."
author: "jpettere"
ms.localizationpriority: high
ms.prod: "users"
doc_type: apiPageType
---

# Get a user

Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Retrieve the properties and relationships of user object.

This operation returns by default only a subset of the more commonly used properties for each user. These _default_ properties are noted in the [Properties](../resources/user.md#properties) section. To get properties that are _not_ returned by default, do a [GET operation](user-get.md) for the user and specify the properties in a `$select` OData query option. Because the **user** resource supports [extensions](/graph/extensibility-overview), you can also use the `GET` operation to get custom properties and extension data in a **user** instance.

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type      | Permissions (from least to most privileged)              |
|:--------------------|:---------------------------------------------------------|
|Delegated (work or school account) | User.Read, User.ReadWrite, User.ReadBasic.All, User.Read.All, User.ReadWrite.All, Directory.Read.All, Directory.ReadWrite.All, Directory.AccessAsUser.All    |
|Delegated (personal Microsoft account) | User.Read, User.ReadWrite    |
|Application | User.Read.All, User.ReadWrite.All, Directory.Read.All, Directory.ReadWrite.All |

Calling the `/me` endpoint requires a signed-in user and therefore a delegated permission. Application permissions are not supported when using the `/me` endpoint.

## HTTP request

For a specific user:
<!-- { "blockType": "ignored" } -->
```http
GET /users/{id | userPrincipalName}
```

>**Note:**
> + When the **userPrincipalName** begins with a `$` character, remove the slash (/) after `/users` and enclose the **userPrincipalName** in parentheses and single quotes. For example, `/users('$AdeleVance@contoso.com')`. For details, see the [known issues](/graph/known-issues#users) list.
> + To query a B2B user using the **userPrincipalName**, encode the hash (#) character. That is, replace the `#` symbol with `%23`. For example, `/users/AdeleVance_adatum.com%23EXT%23@contoso.com`.

For the signed-in user:
<!-- { "blockType": "ignored" } -->
```http
GET /me
```

## Optional query parameters

This method supports the `$select` [OData query parameter](/graph/query-parameters) to retrieve specific user properties, including those that are not returned by default.

## Request headers

| Header       | Value|
|:-----------|:------|
| Authorization  | Bearer {token}. Required.|
| Content-Type   | application/json |

## Request body

Do not supply a request body for this method.

## Response

If successful, this method returns a `200 OK` response code and [user](../resources/user.md) object in the response body. It returns the default properties unless you use `$select` to specify specific properties.

This method returns `202 Accepted` when the request has been processed successfully but the server requires more time to complete related background operations.

## Example

### Example 1: Get the properties of the signed-in user

#### Request


# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "get_user"
}-->
```msgraph-interactive
GET https://graph.microsoft.com/beta/me
```
# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/get-user-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/get-user-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Objective-C](#tab/objc)
[!INCLUDE [sample-code](../includes/snippets/objc/get-user-objc-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/get-user-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Go](#tab/go)
[!INCLUDE [sample-code](../includes/snippets/go/get-user-go-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---

##### Response
Here is an example of the response. Note: The response object shown here might be shortened for readability.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.user"
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json

{
   "displayName": "Adele Vance",
   "givenName": "Adele",
   "jobTitle": "Retail Manager",
   "mail": "AdeleV@contoso.onmicrosoft.com",
   "mobilePhone": "+1 425 555 0109",
   "officeLocation": "18/2111",
   "preferredLanguage": "en-US",
   "surname": "Vance",
   "userPrincipalName": "AdeleV@contoso.onmicrosoft.com",
   "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd"
}
```

### Example 2: Get the properties of the specified user

#### Request

The following example shows a request.


# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "get_other_user"
}-->
```msgraph-interactive
GET https://graph.microsoft.com/beta/users/{id}
```
# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/get-other-user-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/get-other-user-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Objective-C](#tab/objc)
[!INCLUDE [sample-code](../includes/snippets/objc/get-other-user-objc-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/get-other-user-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Go](#tab/go)
[!INCLUDE [sample-code](../includes/snippets/go/get-other-user-go-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---


#### Response

The following example shows the response.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.user"
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json

{
      "displayName": "Adele Vance",
      "givenName": "Adele",
      "jobTitle": "Retail Manager",
      "mail": "AdeleV@contoso.onmicrosoft.com",
      "mobilePhone": "+1 425 555 0109",
      "officeLocation": "18/2111",
      "preferredLanguage": "en-US",
      "surname": "Vance",
      "userPrincipalName": "AdeleV@contoso.onmicrosoft.com",
      "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd"
}
```


### Example 3: Use $select to retrieve specific properties of a user

To retrieve specific properties, use the OData `$select` query parameter. For example, to return _displayName_, _givenName_, _postalCode_, and _identities_, you would use the add the following to your query `$select=displayName,givenName,postalCode,identities`

#### Request


# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "get_user_select"
} -->
```msgraph-interactive
GET https://graph.microsoft.com/v1.0/users/{id | userPrincipalName}?$select=displayName,givenName,postalCode,identities
```
# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/get-user-select-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/get-user-select-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Objective-C](#tab/objc)
[!INCLUDE [sample-code](../includes/snippets/objc/get-user-select-objc-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/get-user-select-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Go](#tab/go)
[!INCLUDE [sample-code](../includes/snippets/go/get-user-select-go-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---


#### Response
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.user"
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users(displayName,givenName,postalCode,identities)/$entity",
    "displayName": "Adele Vance",
    "givenName": "Adele",
    "postalCode": "98004",
    "identities": [
        {
            "signInType": "userPrincipalName",
            "issuer": "contoso.com",
            "issuerAssignedId": "AdeleV@contoso.com"
        }
    ]
}
```

### Example 4: Get the custom security attribute assignments of the specified user

The following example gets the custom security attributes of the specified user.

Attribute #1

+ Attribute set: `Engineering`
+ Attribute: `Project`
+ Attribute data type: Collection of Strings
+ Attribute value: `["Baker","Cascade"]`

Attribute #2

+ Attribute set: `Engineering`
+ Attribute: `CostCenter`
+ Attribute data type: Collection of Integers
+ Attribute value: `[1001]`

Attribute #3

+ Attribute set: `Engineering`
+ Attribute: `Certification`
+ Attribute data type: Boolean
+ Attribute value: `true`

Attribute #4

+ Attribute set: `Marketing`
+ Attribute: `Level`
+ Attribute data type: String
+ Attribute value: `"Public"`

To get custom security attribute assignments, the calling principal must be assigned the Attribute Assignment Reader or Attribute Assignment Administrator role and must be granted the *CustomSecAttributeAssignment.ReadWrite.All* permission.

#### Request



# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "get_user_customsecurityattributes"
}-->
```msgraph-interactive
GET https://graph.microsoft.com/beta/users/{id}?$select=customSecurityAttributes
```
# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/get-user-customsecurityattributes-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/get-user-customsecurityattributes-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Objective-C](#tab/objc)
[!INCLUDE [sample-code](../includes/snippets/objc/get-user-customsecurityattributes-objc-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/get-user-customsecurityattributes-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Go](#tab/go)
[!INCLUDE [sample-code](../includes/snippets/go/get-user-customsecurityattributes-go-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---



#### Response

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.user"
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users(customSecurityAttributes)/$entity",
    "customSecurityAttributes": {
        "Engineering": {
            "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
            "Project@odata.type": "#Collection(String)",
            "Project": [
                "Baker",
                "Cascade"
            ],
            "CostCenter@odata.type": "#Collection(Int32)",
            "CostCenter": [
                1001
            ],
            "Certification": true
        },
        "Marketing": {
            "@odata.type": "#microsoft.graph.customSecurityAttributeValue",
            "Level": "Public"
        }
    }
}
```

If there are no custom security attributes assigned to the user or if the calling principal does not have access, the following will be the response:

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users(customSecurityAttributes)/$entity",
    "customSecurityAttributes": null
}
```

## See also

- [Add custom data to resources using extensions](/graph/extensibility-overview)
- [Add custom data to users using open extensions (preview)](/graph/extensibility-open-users)
- [Add custom data to groups using schema extensions (preview)](/graph/extensibility-schema-groups)

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!--
{
  "type": "#page.annotation",
  "description": "Get user",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": [
  ]
}
-->
